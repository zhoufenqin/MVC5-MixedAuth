# Configuration & Externalized Settings Inventory

The application has a compact configuration surface centered on classic ASP.NET `Web.config`, build configuration in the project file, and package/runtime settings typical of an MVC 5 template. Secrets handling is minimal and mostly implicit through integrated security and commented provider placeholders.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| `Web.config` | Application config | `src/Web.config` | Primary runtime configuration, connection string, app settings, handlers, assembly binding redirects |
| `Web.Debug.config` | Transform | `src/Web.Debug.config` | Debug transform template; no concrete overrides defined |
| `Web.Release.config` | Transform | `src/Web.Release.config` | Release transform removes the `debug` compilation attribute |
| `Views/Web.config` | Razor config | `src/Views/Web.config` | View engine namespaces and Razor-related settings |
| Project file | Build config | `src/MixedAuth.csproj` | Debug/Release properties, IIS Express settings, target framework, references |
| `packages.config` | Dependency config | `src/packages.config` | Declared NuGet package versions |
| OWIN startup | Auth config | `src/Startup.cs`, `src/App_Start/Startup.Auth.cs` | Cookie auth setup and optional external provider hooks |

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| Debug | Default local build | Enables symbols, disables optimization, keeps `debug=true` in base config | MVC web application targets, standard references |
| Release | Manual `Configuration=Release` | Enables optimization and removes `debug` attribute via transform | Same dependency set as Debug |

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| Default | Standard ASP.NET application startup | `Web.config` | LocalDB connection string, no forms auth module, custom Windows login handler |
| Debug transform | Build transform | `Web.Debug.config` + `Web.config` | No effective overrides defined |
| Release transform | Build transform | `Web.Release.config` + `Web.config` | Removes compilation debug flag |

## Properties Inventory

### MixedAuth

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `DefaultConnection` | LocalDB connection string for attached MDF | Default, Debug, Release | `Web.config` connectionStrings |
| `webpages:Version` | `3.0.0.0` | Default, Debug, Release | `Web.config` appSettings |
| `webpages:Enabled` | `false` | Default, Debug, Release | `Web.config` appSettings |
| `ClientValidationEnabled` | `true` | Default, Debug, Release | `Web.config` appSettings |
| `UnobtrusiveJavaScriptEnabled` | `true` | Default, Debug, Release | `Web.config` appSettings |
| `authentication mode` | `None` | Default, Debug, Release | `Web.config` system.web |
| `compilation targetFramework` | `4.5` | Default, Debug, Release | `Web.config` system.web |
| `httpRuntime targetFramework` | `4.5` | Default, Debug, Release | `Web.config` system.web |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| MixedAuth | None explicitly configured in source | Not specified | 1 development instance implied by IIS Express settings |

## Startup Dependency Chain

1. `Startup.ConfigureAuth` configures OWIN application and external sign-in cookies.
2. `MvcApplication.Application_Start` registers areas, filters, routes, and bundles.
3. IIS / ASP.NET starts serving requests.
4. Windows login flows additionally depend on IIS Windows Authentication being enabled before `WindowsLoginHandler` can complete a challenge-response cycle.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage (masked) |
|---|---|---|
| `DefaultConnection` | Database connection string | `Data Source=(LocalDb)\\v11.0;...;Integrated Security=True` |
| External provider client IDs and secrets | OAuth provider credentials | Commented placeholders in `Startup.Auth.cs`, no values committed |

### Secrets Provisioning Workflow

The default configuration relies on integrated security for LocalDB, so no database password is committed. Optional external login providers would require operators to populate the commented OWIN provider settings with client IDs and secrets before deployment; no vault integration, managed identity flow, or automated secret provisioning mechanism was detected.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|

No feature-flag framework or conditional configuration flags were detected.

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| .NET Framework target | 4.5 | `MixedAuth.csproj`, `Web.config` |
| ASP.NET MVC | 5.0.0 | `packages.config` |
| ASP.NET Identity | 1.0.0 | `packages.config` |
| Microsoft OWIN | 2.0.0 | `packages.config` |
| Entity Framework | 6.0.0 | `packages.config` |
| Bootstrap | 3.0.0 | `packages.config` |
| jQuery | 1.10.2 | `packages.config` |
| jQuery Validation | 1.11.1 | `packages.config` |
| Newtonsoft.Json | 5.0.6 | `packages.config` |
