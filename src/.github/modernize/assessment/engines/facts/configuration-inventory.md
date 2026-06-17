# Configuration & Externalized Settings Inventory

The MixedAuth application has a minimal configuration landscape consisting of three Web.config files (one base plus two build-time XML transform overlays) and in-code OWIN startup configuration, with no external config server, secret store, or environment-variable-driven property overrides.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| Web.config | XML application config | `src/Web.config` | Primary runtime config: connection strings, appSettings, HTTP handlers, EF config |
| Web.Debug.config | XML transform | `src/Web.Debug.config` | Applied on Debug build; currently no active transforms (template only) |
| Web.Release.config | XML transform | `src/Web.Release.config` | Applied on Release build; removes `debug` attribute from `compilation` element |
| Views/Web.config | XML view config | `src/Views/Web.config` | Restricts direct HTTP access to Razor view files; sets view engine namespaces |
| Startup.Auth.cs | C# code config | `src/App_Start/Startup.Auth.cs` | OWIN pipeline: configures cookie and external auth middleware |
| RouteConfig.cs | C# code config | `src/App_Start/RouteConfig.cs` | MVC route registration |
| FilterConfig.cs | C# code config | `src/App_Start/FilterConfig.cs` | Global MVC filter registration |
| BundleConfig.cs | C# code config | `src/App_Start/BundleConfig.cs` | CSS and JS bundle definitions |

No external configuration server (Spring Cloud Config, Azure App Configuration), secret store (Azure Key Vault, HashiCorp Vault, AWS Secrets Manager), or Kubernetes ConfigMaps are used.

## Build Profiles

| Profile | Activation | Purpose | Key Changes |
|---|---|---|---|
| Debug | Default (`Configuration=Debug` in MSBuild) | Development build with debug symbols | Outputs debug PDB; `DEBUG` and `TRACE` constants defined; Web.Debug.config transform applied (no active changes) |
| Release | Manual (`Configuration=Release` in MSBuild or publish) | Production/deployment build | Optimized output; `TRACE` constant only; Web.Release.config removes `debug="true"` from compilation; PDB-only symbols |

## Runtime Profiles

This application uses classic ASP.NET (System.Web) on .NET Framework 4.5, which does not support `ASPNETCORE_ENVIRONMENT` or the `appsettings.{Environment}.json` runtime profile system used by ASP.NET Core. There are no runtime profiles. The Web.config transforms are build-time only (applied during MSBuild publish).

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| (Debug build) | MSBuild `Configuration=Debug` | Web.config + Web.Debug.config (no active overrides) | None |
| (Release build) | MSBuild `Configuration=Release` | Web.config + Web.Release.config | Removes `debug="true"` from `<compilation>` |

## Properties Inventory

### MixedAuth Web App — `Web.config`

| Property Key | Default Value | Profiles | Source |
|---|---|---|---|
| ConnectionStrings: DefaultConnection | `Data Source=(LocalDb)\v11.0;AttachDbFilename=|DataDirectory|\MVC5-MixedAuth.mdf;Initial Catalog=MVC5-MixedAuth;Integrated Security=True` | All | Web.config |
| appSettings: webpages:Version | `3.0.0.0` | All | Web.config |
| appSettings: webpages:Enabled | `false` | All | Web.config |
| appSettings: ClientValidationEnabled | `true` | All | Web.config |
| appSettings: UnobtrusiveJavaScriptEnabled | `true` | All | Web.config |
| system.web: authentication mode | `None` | All | Web.config |
| system.web: compilation debug | `true` | Debug only (Release transform removes it) | Web.config |
| system.web: compilation targetFramework | `4.5` | All | Web.config |
| system.web: httpRuntime targetFramework | `4.5` | All | Web.config |
| system.webServer: handler (Windows Login) | path=`Login`, verb=`POST`, type=`MixedAuth.WindowsLoginHandler` | All | Web.config |
| system.webServer: remove FormsAuthenticationModule | (present) | All | Web.config |
| entityFramework: defaultConnectionFactory | `System.Data.Entity.Infrastructure.SqlConnectionFactory` | All | Web.config |
| entityFramework: provider (SQL Server) | `System.Data.Entity.SqlServer.SqlProviderServices` | All | Web.config |
| Assembly binding redirect: System.Web.Mvc | `1.0.0.0–5.0.0.0` → `5.0.0.0` | All | Web.config |
| Assembly binding redirect: System.Web.Helpers | `1.0.0.0–3.0.0.0` → `3.0.0.0` | All | Web.config |
| Assembly binding redirect: System.Web.WebPages | `1.0.0.0–3.0.0.0` → `3.0.0.0` | All | Web.config |
| Assembly binding redirect: WebGrease | `1.0.0.0–1.5.2.14234` → `1.5.2.14234` | All | Web.config |

### OWIN / Authentication (Startup.Auth.cs — code configuration)

| Setting | Value | Notes |
|---|---|---|
| Cookie auth type | `DefaultAuthenticationTypes.ApplicationCookie` | Standard OWIN cookie auth |
| Cookie login path | `/Account/Login` | Redirect target for unauthenticated requests |
| External sign-in cookie type | `DefaultAuthenticationTypes.ExternalCookie` | Temporary cookie for OAuth flow |
| IIS Express: AnonymousAuthentication | `enabled` | Allows anonymous access to serve login pages |
| IIS Express: WindowsAuthentication | `enabled` | Enables IIS-level Windows auth for the Windows login handler |

## Startup Parameters & Resource Requirements

| Service | Runtime Options | Memory | Instance Count |
|---|---|---|---|
| MixedAuth Web App | None specified (hosted in IIS Express for dev, IIS for prod) | Not configured | 1 (no scaling config) |

No JVM parameters are applicable (.NET Framework). No Docker, Kubernetes, or cloud deployment manifests are present. IIS/IIS Express hosting settings are in the `.csproj` project file (port 3314 for IIS Express dev).

## Startup Dependency Chain

The application has a simple single-service startup: IIS/IIS Express loads the ASP.NET application → OWIN pipeline initializes (`Startup.Configuration`) → `Startup.Auth.cs` registers cookie middleware → Entity Framework lazy-initializes the database connection on first user operation.

No explicit startup dependency ordering, health-check probes, `dockerize` wait-for-TCP, or readiness endpoints are configured. The application will fail at runtime (first DB request) if SQL Server is unavailable, with no graceful degradation or retry.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage |
|---|---|---|
| DefaultConnection (connection string) | Database connection | Web.config plaintext — uses Integrated Security (no password) |
| External OAuth client IDs and secrets | OAuth credentials | Commented-out in Startup.Auth.cs; would need to be added to Web.config or environment variables if enabled |

The connection string uses Windows Integrated Security (`Integrated Security=True`), so no database password is stored. However, if external OAuth providers (Facebook, Google, Twitter, Microsoft Account) are enabled, client IDs and secrets would be embedded in `Startup.Auth.cs` or `Web.config` in plaintext — no secret management integration is in place.

### Secrets Provisioning Workflow

No formal secrets provisioning workflow exists. The application stores all configuration (including what would be credentials) directly in `Web.config`. For production deployments:

- The database connection string should be replaced with a production SQL Server connection string, injected via web.config transforms, environment variables, or IIS application settings.
- If OAuth providers are enabled, client secrets must be manually placed in `Web.config` or read from environment variables (no Key Vault, Vault, or Secrets Manager integration is implemented).
- No CI/CD pipeline configuration for secret injection is present in the repository.

## Feature Flags

No feature flag framework is used. The OAuth external login providers are effectively "feature-flagged" by being commented out in `Startup.Auth.cs`, but this is a code-level toggle requiring a rebuild/redeploy — not a runtime feature flag.

| Flag Name | Default | Controlled By |
|---|---|---|
| Microsoft Account OAuth | Disabled (commented out) | Code change in Startup.Auth.cs |
| Twitter OAuth | Disabled (commented out) | Code change in Startup.Auth.cs |
| Facebook OAuth | Disabled (commented out) | Code change in Startup.Auth.cs |
| Google OAuth | Disabled (commented out) | Code change in Startup.Auth.cs |

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| .NET Framework (runtime target) | 4.5 | Web.config, MixedAuth.csproj |
| ASP.NET MVC | 5.0.0 | packages.config |
| ASP.NET Razor | 3.0.0 | packages.config |
| ASP.NET WebPages | 3.0.0 | packages.config |
| ASP.NET Web Optimization | 1.1.1 | packages.config |
| OWIN (Katana) | 2.0.0 | packages.config |
| Microsoft.Owin | 2.0.0 | packages.config |
| Microsoft.Owin.Host.SystemWeb | 2.0.0 | packages.config |
| Microsoft.Owin.Security | 2.0.0 | packages.config |
| ASP.NET Identity Core | 1.0.0 | packages.config |
| ASP.NET Identity EntityFramework | 1.0.0 | packages.config |
| ASP.NET Identity Owin | 1.0.0 | packages.config |
| Entity Framework | 6.0.0 | packages.config |
| Newtonsoft.Json | 5.0.6 | packages.config |
| Bootstrap | 3.0.0 | packages.config |
| jQuery | 1.10.2 | packages.config |
| Build tool | MSBuild (Visual Studio 2013 / ToolsVersion 12.0) | MixedAuth.csproj |
| IIS Express (dev server) | Default (VS-bundled) | MixedAuth.csproj |
