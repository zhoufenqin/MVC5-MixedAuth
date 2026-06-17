# MixedAuth

## Summary

| Metric | Value |
|--------|-------|
| Total Issues | 20 |
| Mandatory Blockers | 10 |
| Potential Issues | 4 |

## Component Information

| Property | Value |
|----------|-------|
| Language | C# |
| Frameworks | .NETFramework,Version=v4.5 |
| Build tools | MSBuild |

## Cloud Readiness Issues

| Issue Name | Criticality | Story Points | Occurrences |
|------------|-------------|--------------|-------------|
| Windows authentication detected | Mandatory | 3 | [1](#Windows_authentication_detected) |
| Old .NET Framework dependency detected | Potential | 3 | [1](#Old_NET_Framework_dependency_detected) |
| SQL database connection detected | Potential | 3 | [1](#SQL_database_connection_detected) |
| Hardcoded sensitive data detected | Optional | 3 | [14](#Hardcoded_sensitive_data_detected) |
| Static content detected | Optional | 3 | [1](#Static_content_detected) |
| System.Data.SqlClient dependency detected | Optional | 3 | [1](#System_Data_SqlClient_dependency_detected) |
| Connection strings without configuration builders detected | Optional | 3 | [1](#Connection_strings_without_configuration_builders_detected) |

### Issue Details

<details id="Windows_authentication_detected">
<summary><b>Windows authentication detected</b> — affected files</summary>

- `Web.config`

</details>

<details id="Old_NET_Framework_dependency_detected">
<summary><b>Old .NET Framework dependency detected</b> — affected files</summary>

- `MixedAuth.csproj`

</details>

<details id="SQL_database_connection_detected">
<summary><b>SQL database connection detected</b> — affected files</summary>

- `Web.config`

</details>

<details id="Hardcoded_sensitive_data_detected">
<summary><b>Hardcoded sensitive data detected</b> — affected files</summary>

- `Controllers\AccountController.cs (line 158)`
- `Controllers\AccountController.cs (line 55)`
- `Controllers\AccountController.cs (line 121)`
- `Controllers\AccountController.cs (line 122)`
- `Models\AccountViewModels.cs (line 25)`
- `Models\AccountViewModels.cs (line 58)`
- `Models\AccountViewModels.cs (line 15)`
- `Models\AccountViewModels.cs (line 21)`
- `Models\AccountViewModels.cs (line 26)`
- `Models\AccountViewModels.cs (line 38)`
- `Models\AccountViewModels.cs (line 54)`
- `Models\AccountViewModels.cs (line 59)`
- `Models\AccountViewModels.cs (line 26)`
- `Models\AccountViewModels.cs (line 59)`

</details>

<details id="Static_content_detected">
<summary><b>Static content detected</b> — affected files</summary>

- `MixedAuth.csproj`

</details>

<details id="System_Data_SqlClient_dependency_detected">
<summary><b>System.Data.SqlClient dependency detected</b> — affected files</summary>

- `Web.config`

</details>

<details id="Connection_strings_without_configuration_builders_detected">
<summary><b>Connection strings without configuration builders detected</b> — affected files</summary>

- `Web.config`

</details>

## DotNET Upgrade Issues [View Details](scenarios/dotnet-version-upgrade/assessment.md)

| Issue Category | Criticality | Story Points | Occurrences |
|----------------|-------------|--------------|-------------|
| Binary incompatible for selected .NET version | Mandatory | 1 | [40](#Binary_incompatible_for_selected_NET_version) |
| NuGet package is incompatible | Mandatory | 1 | [14](#NuGet_package_is_incompatible) |
| System.Web.Optimization bundling and minification is not supported in .NET Core and should be replaced with actual html tags pointing to content files | Mandatory | 1 | [6](#System_Web_Optimization_bundling_and_minification_is_not_supported_in_NET_Core_and_should_be_replaced_with_actual_html_tags_pointing_to_content_files) |
| NuGet package functionality is included with framework reference | Mandatory | 1 | [4](#NuGet_package_functionality_is_included_with_framework_reference) |
| Routes registration via RouteCollection is not supported in .NET Core and needs to be converted to the route mappings on the application object | Mandatory | 1 | [2](#Routes_registration_via_RouteCollection_is_not_supported_in_NET_Core_and_needs_to_be_converted_to_the_route_mappings_on_the_application_object) |
| Project file needs to be converted to SDK-style | Mandatory | 1 | [1](#Project_file_needs_to_be_converted_to_SDK-style) |
| Project's target framework(s) needs to be changed | Mandatory | 1 | [1](#Project_s_target_framework_s_needs_to_be_changed) |
| Convert application initialization code from Global.asax.cs to .NET Core and clean up Global.asax.cs | Mandatory | 1 | [1](#Convert_application_initialization_code_from_Global_asax_cs_to_NET_Core_and_clean_up_Global_asax_cs) |
| ASP.NET Framework (System.Web) | Mandatory | 4 | 0 |
| Source incompatible for selected .NET version | Potential | 1 | [71](#Source_incompatible_for_selected_NET_version) |
| NuGet package upgrade is recommended | Potential | 1 | [3](#NuGet_package_upgrade_is_recommended) |
| NuGet package is deprecated | Optional | 1 | [11](#NuGet_package_is_deprecated) |
| NuGet package contains security vulnerability | Optional | 1 | [7](#NuGet_package_contains_security_vulnerability) |

### Issue Details

<details id="Binary_incompatible_for_selected_NET_version">
<summary><b>Binary incompatible for selected .NET version</b> — affected files</summary>

- `Windows\WindowsLoginHandler.cs (line 112, col 4)`
- `Windows\WindowsLoginHandler.cs (line 115, col 6)`
- `Windows\WindowsLoginHandler.cs (line 101, col 6)`
- `Windows\WindowsLoginHandler.cs (line 89, col 6)`
- `Windows\WindowsLoginHandler.cs (line 77, col 6)`
- `Windows\WindowsLoginHandler.cs (line 76, col 6)`
- `Windows\WindowsLoginHandler.cs (line 74, col 6)`
- `Windows\MixedAuthExtensions.cs (line 83, col 4)`
- `Windows\MixedAuthExtensions.cs (line 100, col 10)`
- `Windows\MixedAuthExtensions.cs (line 99, col 10)`
- `Windows\MixedAuthExtensions.cs (line 96, col 10)`
- `Windows\MixedAuthExtensions.cs (line 95, col 10)`
- `Windows\MixedAuthExtensions.cs (line 92, col 10)`
- `Windows\MixedAuthExtensions.cs (line 91, col 10)`
- `Windows\MixedAuthExtensions.cs (line 86, col 6)`
- `Windows\MixedAuthExtensions.cs (line 85, col 6)`
- `Windows\MixedAuthExtensions.cs (line 47, col 4)`
- `Global.asax.cs (line 21, col 6)`
- `App_Start\RouteConfig.cs (line 11, col 4)`

</details>

<details id="NuGet_package_is_incompatible">
<summary><b>NuGet package is incompatible</b> — affected files</summary>

- `MixedAuth.csproj`

</details>

<details id="System_Web_Optimization_bundling_and_minification_is_not_supported_in_NET_Core_and_should_be_replaced_with_actual_html_tags_pointing_to_content_files">
<summary><b>System.Web.Optimization bundling and minification is not supported in .NET Core and should be replaced with actual html tags pointing to content files</b> — affected files</summary>

- `Views\Account\ExternalLoginConfirmation.cshtml`
- `Views\Account\Login.cshtml`
- `Views\Account\Manage.cshtml`
- `Views\Account\Register.cshtml`
- `Views\Account\WindowsLoginConfirmation.cshtml`
- `Views\Shared\_Layout.cshtml`

</details>

<details id="NuGet_package_functionality_is_included_with_framework_reference">
<summary><b>NuGet package functionality is included with framework reference</b> — affected files</summary>

- `MixedAuth.csproj`

</details>

<details id="Routes_registration_via_RouteCollection_is_not_supported_in_NET_Core_and_needs_to_be_converted_to_the_route_mappings_on_the_application_object">
<summary><b>Routes registration via RouteCollection is not supported in .NET Core and needs to be converted to the route mappings on the application object</b> — affected files</summary>

- `Global.asax.cs`
- `App_Start\RouteConfig.cs`

</details>

<details id="Project_file_needs_to_be_converted_to_SDK-style">
<summary><b>Project file needs to be converted to SDK-style</b> — affected files</summary>

- `MixedAuth.csproj`

</details>

<details id="Project_s_target_framework_s_needs_to_be_changed">
<summary><b>Project's target framework(s) needs to be changed</b> — affected files</summary>

- `MixedAuth.csproj`

</details>

<details id="Convert_application_initialization_code_from_Global_asax_cs_to_NET_Core_and_clean_up_Global_asax_cs">
<summary><b>Convert application initialization code from Global.asax.cs to .NET Core and clean up Global.asax.cs</b> — affected files</summary>

- `Global.asax.cs`

</details>

<details id="Source_incompatible_for_selected_NET_version">
<summary><b>Source incompatible for selected .NET version</b> — affected files</summary>

- `Controllers\AccountController.Windows.cs (line 91, col 6)`
- `Windows\WindowsLoginHandler.cs (line 112, col 4)`
- `Windows\WindowsLoginHandler.cs (line 114, col 6)`
- `Windows\WindowsLoginHandler.cs (line 99, col 4)`
- `Windows\WindowsLoginHandler.cs (line 87, col 4)`
- `Windows\WindowsLoginHandler.cs (line 72, col 4)`
- `Windows\WindowsLoginHandler.cs (line 77, col 6)`
- `Windows\WindowsLoginHandler.cs (line 76, col 6)`
- `Windows\WindowsLoginHandler.cs (line 29, col 4)`
- `Windows\WindowsLoginHandler.cs (line 48, col 11)`
- `Windows\WindowsLoginHandler.cs (line 42, col 8)`
- `Windows\WindowsLoginHandler.cs (line 40, col 6)`
- `Windows\WindowsLoginHandler.cs (line 31, col 6)`
- `Windows\WindowsLoginHandler.cs (line 28, col 38)`
- `Windows\WindowsLoginHandler.cs (line 28, col 33)`
- `Windows\WindowsLoginHandler.cs (line 28, col 4)`
- `Windows\WindowsLoginHandler.cs (line 26, col 37)`
- `Windows\WindowsLoginHandler.cs (line 26, col 83)`
- `Windows\MixedAuthExtensions.cs (line 169, col 6)`
- `Windows\MixedAuthExtensions.cs (line 164, col 6)`
- `Windows\MixedAuthExtensions.cs (line 153, col 6)`
- `Windows\MixedAuthExtensions.cs (line 142, col 6)`
- `Windows\MixedAuthExtensions.cs (line 126, col 4)`
- `Windows\MixedAuthExtensions.cs (line 132, col 6)`
- `Windows\MixedAuthExtensions.cs (line 131, col 6)`
- `Windows\MixedAuthExtensions.cs (line 128, col 6)`
- `Windows\MixedAuthExtensions.cs (line 117, col 6)`
- `Windows\MixedAuthExtensions.cs (line 114, col 6)`
- `Windows\MixedAuthExtensions.cs (line 65, col 4)`
- `Windows\MixedAuthExtensions.cs (line 70, col 8)`
- `Windows\MixedAuthExtensions.cs (line 69, col 8)`
- `Windows\MixedAuthExtensions.cs (line 67, col 6)`
- `Windows\MixedAuthExtensions.cs (line 56, col 4)`
- `Windows\MixedAuthExtensions.cs (line 58, col 6)`
- `Windows\MixedAuthExtensions.cs (line 39, col 8)`
- `Windows\MixedAuthExtensions.cs (line 37, col 6)`
- `Global.asax.cs (line 12, col 4)`
- `Global.asax.cs (line 10, col 43)`

</details>

<details id="NuGet_package_upgrade_is_recommended">
<summary><b>NuGet package upgrade is recommended</b> — affected files</summary>

- `MixedAuth.csproj`

</details>

<details id="NuGet_package_is_deprecated">
<summary><b>NuGet package is deprecated</b> — affected files</summary>

- `MixedAuth.csproj`

</details>

<details id="NuGet_package_contains_security_vulnerability">
<summary><b>NuGet package contains security vulnerability</b> — affected files</summary>

- `MixedAuth.csproj`

</details>

---

## Codebase Insights

> **Note:** These documents are generated by AI and may contain inaccuracies or incomplete information. Please review carefully.

1. **[Architecture Diagram](facts/architecture-diagram.md)** — Understand the big picture: system layers and component relationships
2. **[Dependency Map](facts/dependency-map.md)** — Know what the project depends on and where the risks are
3. **[API & Service Contracts](facts/api-service-contracts.md)** — See how services communicate and what contracts they expose
4. **[Data Architecture](facts/data-architecture.md)** — Explore data models, storage, and data flow patterns
5. **[Configuration Inventory](facts/configuration-inventory.md)** — Review how the application is configured across environments
6. **[Business Workflows](facts/business-workflows.md)** — Trace end-to-end business processes and domain logic

[Share feedback](https://aka.ms/ghcp-appmod/feedback)
