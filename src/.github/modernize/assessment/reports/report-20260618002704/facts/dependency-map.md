# Dependency Map

This document summarizes the declared external dependencies for the MixedAuth web application. The project declares 24 primary packages in `packages.config`, centered on the ASP.NET MVC 5, OWIN, and Entity Framework 6 stack.

## Dependencies

```mermaid
flowchart LR
    App["MixedAuth"]

    subgraph Web["Web Frameworks"]
        Mvc["ASP.NET MVC 5.0.0"]
        Razor["ASP.NET Razor 3.0.0"]
        WebPages["ASP.NET WebPages 3.0.0"]
        Optimize["Web Optimization 1.1.1"]
    end
    subgraph DB["Database and ORM"]
        EF["Entity Framework 6.0.0"]
    end
    subgraph Log["Security"]
        IdentityCore["Identity Core 1.0.0"]
        IdentityEf["Identity EntityFramework 1.0.0"]
        IdentityOwin["Identity OWIN 1.0.0"]
        OwinCore["OWIN 1.0"]
        Owin["Microsoft OWIN 2.0.0"]
        Host["OWIN Host SystemWeb 2.0.0"]
        Cookies["OWIN Security Cookies 2.0.0"]
        OAuth["OWIN Security OAuth 2.0.0"]
        Facebook["OWIN Facebook 2.0.0"]
        Google["OWIN Google 2.0.0"]
        Twitter["OWIN Twitter 2.0.0"]
        MicrosoftAccount["OWIN MicrosoftAccount 2.0.0"]
    end
    subgraph Util["Utilities"]
        Json["Newtonsoft Json 5.0.6"]
        WebInfra["Web Infrastructure 1.0.0.0"]
        Antlr["Antlr 3.4.1.9004"]
        WebGrease["WebGrease 1.5.2"]
    end
    subgraph Client["Client Assets"]
        Bootstrap["Bootstrap 3.0.0"]
        JQuery["jQuery 1.10.2"]
        JQueryVal["jQuery Validation 1.11.1"]
        Unobtrusive["jQuery Unobtrusive Validation 3.0.0"]
        Modernizr["Modernizr 2.6.2"]
        Respond["Respond 1.2.0"]
    end

    App -->|"web"| Web
    App -->|"identity data"| DB
    App -->|"authentication"| Log
    App -->|"utility libs"| Util
    App -->|"browser assets"| Client
    IdentityCore -.->|"used by"| IdentityEf
    OwinCore -.->|"abstractions"| Owin
    Owin -.->|"runtime host"| Host
```

### Dependency Summary

| Category | Count | Key Libraries | Notes |
|---|---|---|---|
| Web Frameworks | 4 | ASP.NET MVC 5.0.0, Razor 3.0.0 | Classic ASP.NET MVC 5 stack on .NET Framework 4.5 |
| Database / ORM | 1 | Entity Framework 6.0.0 | Identity data access only; no custom domain ORM layer |
| Security | 11 | ASP.NET Identity, Microsoft.Owin, provider packages | Mixed local, Windows, and optional external authentication |
| Utilities | 4 | Newtonsoft.Json 5.0.6, WebGrease 1.5.2 | Older support libraries typical of the MVC 5 template era |
| Client Assets | 6 | Bootstrap 3.0.0, jQuery 1.10.2 | Legacy front-end libraries bundled with the application |

### Version & Compatibility Risks

The dependency set is strongly tied to .NET Framework 4.5-era ASP.NET MVC 5 packages. Entity Framework 6, ASP.NET Identity 1.x, and OWIN 2.0.0 all have upgrade paths, but they require modernization work because the project is not based on ASP.NET Core or SDK-style project conventions. Several client libraries such as jQuery 1.10.2, Bootstrap 3.0.0, and Newtonsoft.Json 5.0.6 are substantially outdated.

### Notable Observations

- Authentication concerns dominate the dependency graph, which matches the repository's mixed-auth proof-of-concept focus.
- External provider packages for Facebook, Google, Twitter, and Microsoft Account are declared even though the startup configuration leaves them commented out by default.
- The project uses `packages.config` rather than SDK-style `PackageReference`, which increases migration friction for newer .NET targets.
- There are no dedicated observability, caching, or messaging libraries declared.

## Test Dependencies

| Framework | Version | Notes |
|---|---|---|

Total test-scope dependencies: 0

No test dependencies detected. The repository does not contain a separate automated test project or test-specific NuGet packages.
