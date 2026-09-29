# SPFx Quick Reference

[Back to Awesome SPFx](../README.md) · [Practical tips](tips-and-tricks.md)

This reference targets the Heft-based toolchain used by SPFx v1.22 and later. SPFx pins its Node.js, TypeScript, and React versions, so check the official compatibility matrix in the [resource directory](../README.md#official-documentation) before creating or upgrading a project. In particular, install React and React DOM with `--save-exact`; an incompatible React version can build successfully and still fail at runtime.

## Getting Started

| Step                     | What to do                                                                                                                                                            |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. Prepare a tenant      | Use a Microsoft 365 tenant where you can test SharePoint pages and, for deployment, access an app catalog.                                                            |
| 2. Install Node.js       | Install the Node.js LTS version required by your chosen SPFx release. SPFx v1.22-v1.23 use Node.js 22.                                                                |
| 3. Install the toolchain | Run `npm install @rushstack/heft yo @microsoft/generator-sharepoint --global`.                                                                                        |
| 4. Create a project      | Create an empty directory, enter it, and run `yo @microsoft/sharepoint`. Choose the component type, name, framework, and target environment when prompted.            |
| 5. Trust HTTPS locally   | From the generated project, run `heft trust-dev-cert` once per development machine.                                                                                   |
| 6. Start development     | Run `heft start` to build, watch for changes, host local bundles, and open the SharePoint-hosted workbench.                                                           |
| 7. Test in SharePoint    | Test web parts in the hosted workbench and real modern pages. Test extensions on a real page with the SPFx Debug Toolbar because the workbench does not support them. |
| 8. Package for release   | Run `heft build --production`, followed by `heft package-solution --production`.                                                                                      |
| 9. Deploy                | Upload the `.sppkg` from the path configured in `config/package-solution.json` to the app catalog, deploy it, and add the app to a site unless it is tenant-wide.     |

Optional: set `SPFX_SERVE_TENANT_DOMAIN` to your tenant domain or test-site URL so `{tenantDomain}` in `config/serve.json` resolves automatically.

```text
# PowerShell
$env:SPFX_SERVE_TENANT_DOMAIN = "contoso.sharepoint.com"

# macOS or Linux
export SPFX_SERVE_TENANT_DOMAIN="contoso.sharepoint.com"
```

## Command Cheat Sheet

| Task                               | Heft command                         | Legacy gulp equivalent         |
| ---------------------------------- | ------------------------------------ | ------------------------------ |
| Show available actions             | `heft --help`                        | `gulp --tasks`                 |
| Trust the development certificate  | `heft trust-dev-cert`                | `gulp trust-dev-cert`          |
| Remove the development certificate | `heft untrust-dev-cert`              | `gulp untrust-dev-cert`        |
| Start local development            | `heft start`                         | `gulp serve`                   |
| Build development bundles          | `heft build`                         | `gulp build` and `gulp bundle` |
| Build production bundles           | `heft build --production`            | `gulp bundle --ship`           |
| Run configured tests               | `heft test`                          | `gulp test`                    |
| Clean generated output             | `heft clean`                         | `gulp clean`                   |
| Package a solution                 | `heft package-solution --production` | `gulp package-solution --ship` |
| Test assets from a development CDN | `heft dev-deploy`                    | No direct equivalent.          |
| Deploy assets to Azure Storage     | `heft deploy-azure-storage`          | `gulp deploy-azure-storage`    |

Heft combines the old `build` and `bundle` tasks into `heft build`, and replaces the legacy `--ship` flag with `--production`.

## Project Structure

| Path                           | Purpose                                                                                           |
| ------------------------------ | ------------------------------------------------------------------------------------------------- |
| `config/package-solution.json` | Solution metadata, feature configuration, deployment settings, version, and `.sppkg` output path. |
| `config/serve.json`            | Local server and debug-page configuration.                                                        |
| `config/rig.json`              | Points Heft to the standard `@microsoft/spfx-web-build-rig` configuration.                        |
| `sharepoint/assets/`           | Optional elements, schema, and upgrade XML used to provision SharePoint assets.                   |
| `sharepoint/solution/`         | Default output directory for the packaged `.sppkg` file.                                          |
| `src/webparts/`                | Client-side web part source, styles, localization, components, and manifest files.                |
| `src/extensions/`              | Application Customizer, Field Customizer, Command Set, and Form Customizer source files.                           |
| `src/adaptiveCardExtensions/`  | Adaptive Card Extension source, card views, and quick views.                                      |
| `teams/`                       | Optional Microsoft Teams app package assets.                                                      |
| `package.json`                 | npm dependencies and project scripts. Keep SPFx framework package versions aligned.               |
| `tsconfig.json`                | TypeScript compiler configuration inherited by the project.                                       |

Useful web-part context members:

| Member                              | Typical use                                                    |
| ----------------------------------- | -------------------------------------------------------------- |
| `this.context.pageContext`          | Current site, web, list, item, culture, and user information.  |
| `this.context.spHttpClient`         | Authenticated SharePoint REST requests.                        |
| `this.context.msGraphClientFactory` | Authenticated Microsoft Graph clients.                         |
| `this.context.aadHttpClientFactory` | Calls to Microsoft Entra ID-protected APIs.                    |
| `this.context.sdks.microsoftTeams`  | Microsoft Teams host context when the component runs in Teams. |
| `this.context.serviceScope`         | Shared SPFx services and dependency injection.                 |
| `this.context.propertyPane`         | Web-part property-pane operations.                             |
| `this.domElement`                   | The DOM element owned by the current web-part instance.        |

## Glossary

| Term                          | Meaning                                                                                                                |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Adaptive Card Extension (ACE) | A Viva Connections component with card views and quick views, optimized for focused dashboard interactions.            |
| App catalog                   | A tenant-level or site-collection library used to deploy and manage SharePoint solution packages.                      |
| Application Customizer        | An extension that runs on modern pages and can render UI in supported placeholders such as the page header or footer.  |
| Command Set                   | An extension that adds commands to list and library toolbars and item context menus.                                   |
| Component manifest            | A JSON file that defines a component's ID, type, version, supported hosts, and loader metadata.                        |
| Field Customizer              | An extension that changes how a field is rendered in a modern list view.                                               |
| Heft                          | The task runner and configurable build system used by SPFx v1.22 and later.                                            |
| Hosted workbench              | A SharePoint-hosted page used to preview web parts and ACEs while loading bundles from the local development server.   |
| Microsoft Graph               | The unified API for Microsoft 365 data and services.                                                                   |
| PnP                           | Microsoft 365 & Power Platform Community guidance, samples, libraries, and tooling.                                    |
| Property pane                 | The configuration UI displayed when a page author edits a web part.                                                    |
| SharePoint Framework (SPFx)   | Microsoft's client-side extensibility model for SharePoint, Teams, Outlook, and Viva Connections.                      |
| Solution package (`.sppkg`)   | The deployable archive containing manifests, package metadata, and optionally client-side assets and provisioning XML. |
| Tenant-wide deployment        | Deployment mode that makes eligible components available without requiring the app to be installed on every site.      |
| Web part                      | A configurable client-side component that a page author can place on a SharePoint page.                                |

## FAQ and Troubleshooting

| Symptom                                         | What to check                                                                                                                                                                             |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `heft` is not recognized                        | Install `@rushstack/heft` globally, or run the project-local CLI with `npx @rushstack/heft`. Always run commands from the project root after `npm install`.                               |
| The generator or build rejects Node.js          | Compare `node --version` with the compatibility matrix. Use a Node version manager when maintaining projects on different SPFx releases.                                                  |
| The browser rejects the local HTTPS certificate | Run `heft untrust-dev-cert`, followed by `heft trust-dev-cert`, then restart the browser. If workstation policy blocks certificate trust, follow Microsoft's manual certificate guidance. |
| The hosted workbench opens the wrong tenant     | Set `SPFX_SERVE_TENANT_DOMAIN`, or update the `initialPage` in `config/serve.json` for the project.                                                                                       |
| `manifests.js` returns 404                      | Keep `heft start` running, confirm `https://localhost:4321` loads without a certificate warning, and verify the debug-manifest URL and port.                                              |
| The build succeeds but the component is blank   | Check the browser console first. Verify exact React and React DOM versions, ensure the component's supported hosts are correct, and inspect failed network requests.                      |
| React reports an invalid hook call              | Confirm that `react` and `react-dom` exactly match the versions supported by the SPFx release and that a library did not bundle a second React copy.                                      |
| An extension cannot be tested in the workbench  | This is expected. Start the local server and debug it on a real modern SharePoint page using the debug query string and SPFx Debug Toolbar.                                               |
| API calls return 401 or 403                     | Confirm the current user's permissions, the requested resource URL, declared API permissions, and tenant-admin approval in SharePoint administration.                                     |
| A new package behaves like the previous version | Increase the solution version in `config/package-solution.json`, rebuild and repackage with `--production`, redeploy the `.sppkg`, and clear stale browser or CDN caches.                 |
| npm reports audit warnings                      | Do not blindly run `npm audit fix`, because it can install framework dependencies that SPFx has not validated. Check the current SPFx release notes and upgrade deliberately.             |

## Best Practices

| Area                    | Guidance                                                                                                                                                                                                          |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Compatibility           | Treat the compatibility matrix as authoritative. Pin React exactly, keep all `@microsoft/sp-*` packages aligned, and avoid opportunistic dependency upgrades.                                                     |
| Architecture            | Keep SharePoint and Graph access in services, UI state in components or hooks, and host-specific behavior behind small adapters. Avoid global mutable state because multiple web-part instances can share a page. |
| Lifecycle               | Initialize shared services in `onInit`, render only into the component's owned DOM element, and release subscriptions, timers, observers, and event handlers in `onDispose`.                                      |
| Performance             | Request only required fields, use `$select`, `$filter`, pagination, and batching where supported, cache stable reference data, and lazy-load expensive features. Avoid network calls directly from `render()`.    |
| Security                | Never ship secrets in a client-side bundle. Use Microsoft Entra ID and SPFx HTTP clients, request least-privilege permissions, escape or sanitize untrusted content, and avoid dynamic script injection.          |
| Content Security Policy | Bundle dependencies when practical, minimize external script origins, and test the solution against SharePoint Online CSP behavior before deployment.                                                             |
| Accessibility           | Use semantic HTML, keyboard-accessible interactions, visible focus states, meaningful labels, and sufficient color contrast. Test with zoom and a screen reader.                                                  |
| Theming                 | Use SharePoint or Fluent UI theme tokens instead of fixed colors, and respond to theme changes and dark mode where supported.                                                                                     |
| Localization            | Store user-facing strings in locale files and use SharePoint culture information for dates, numbers, and time zones.                                                                                              |
| Error handling          | Give users a useful state for loading, empty results, partial failures, and permission errors. Log diagnostic detail without exposing sensitive information.                                                      |
| Testing                 | Unit-test services and state logic, test production bundles on real modern pages, and verify every declared host such as SharePoint, Teams, Outlook, or Viva Connections.                                         |
| Packaging               | Build and package with `--production`, keep solution and feature versions intentional, and validate upgrade paths before replacing a deployed package.                                                            |
| Toolchain customization | Prefer the standard SPFx rig and supported Heft plugins. Ejecting the Webpack configuration is a one-way operation that removes Microsoft support for the toolchain.                                              |
| Maintenance             | Document the supported SPFx version, use CI for linting, tests, and production builds, and review official release notes before upgrading.                                                                        |

## Further Reading

- [SPFx compatibility matrix](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/compatibility) - Supported Node.js, TypeScript, and React versions.
- [Development environment setup](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-development-environment) - Current installation and certificate-trust instructions.
- [Heft toolchain](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/toolchain/sharepoint-framework-toolchain-rushstack-heft) - Toolchain behavior, customization, and migration context.
- [Debug Toolbar](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/debug-toolbar) - Inspect components on actual SharePoint pages.

For step-by-step learning, common pitfalls, and release checks, continue with [tips and tricks](tips-and-tricks.md).
