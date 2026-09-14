# Awesome SPFx [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Client-side development framework for extending SharePoint, Microsoft Teams, Outlook, and Viva Connections with web parts, extensions, and Adaptive Card Extensions.

The **SharePoint Framework (SPFx)** is Microsoft's page and web part development model for building client-side web parts, extensions, and Adaptive Card Extensions that run in SharePoint, Microsoft Teams, Outlook, and Viva Connections. It's built on modern web tooling (TypeScript, npm, Webpack) and is the recommended way to extend SharePoint and Microsoft 365 with custom UI.

This list is for developers who are new to SPFx and want a map of the ecosystem, as well as experienced developers looking for well-maintained libraries, tools, and community resources.

There isn't a lot of curated, up-to-date documentation specifically for the SPFx ecosystem; most resources are scattered across official docs, blogs, and GitHub repositories. This list brings the best of them together in one place.

## Contents

- [SPFx Quick Reference](#spfx-quick-reference)
- [Official Docs & Resources](#official-docs--resources)
- [Environment Setup Notes](#environment-setup-notes)
- [Getting Started / Generators](#getting-started--generators)
- [PnP Libraries](#pnp-libraries)
- [Sample Galleries](#sample-galleries)
- [Dev Tools & VS Code Extensions](#dev-tools--vs-code-extensions)
- [SharePoint Migration Tools](#sharepoint-migration-tools)
- [Boilerplates & Starters](#boilerplates--starters)
- [Testing & CI/CD](#testing--cicd)
- [AI / Copilot Integrations](#ai--copilot-integrations)
- [Learning Resources](#learning-resources)
- [Video Tutorials](#video-tutorials)
- [Community](#community)

## SPFx Quick Reference

This reference targets the Heft-based toolchain used by SPFx v1.22 and later. SPFx pins its Node.js, TypeScript, and React versions, so check the official compatibility matrix under Official Docs & Resources before creating or upgrading a project. In particular, install React and React DOM with `--save-exact`; an incompatible React version can build successfully and still fail at runtime.

### Getting Started

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

### Command Cheat Sheet

| Task                               | Heft command                         | Legacy gulp equivalent         |
| ---------------------------------- | ------------------------------------ | ------------------------------ |
| Show available actions             | `heft --help`                        | `gulp --tasks`                 |
| Trust the development certificate  | `heft trust-dev-cert`                | `gulp trust-dev-cert`          |
| Remove the development certificate | `heft untrust-dev-cert`              | `gulp untrust-dev-cert`        |
| Start local development            | `heft start`                         | `gulp serve`                   |
| Build development bundles          | `heft build`                         | `gulp build` and `gulp bundle` |
| Build production bundles           | `heft build --production`            | `gulp bundle --ship`           |
| Run tests                          | `heft test`                          | `gulp test`                    |
| Clean generated output             | `heft clean`                         | `gulp clean`                   |
| Package a solution                 | `heft package-solution --production` | `gulp package-solution --ship` |
| Test assets from a development CDN | `heft dev-deploy`                    | No direct equivalent.          |
| Deploy assets to Azure Storage     | `heft deploy-azure-storage`          | `gulp deploy-azure-storage`    |

Heft combines the old `build` and `bundle` tasks into `heft build`, and replaces the legacy `--ship` flag with `--production`.

### Project Structure

| Path                           | Purpose                                                                                           |
| ------------------------------ | ------------------------------------------------------------------------------------------------- |
| `config/package-solution.json` | Solution metadata, feature configuration, deployment settings, version, and `.sppkg` output path. |
| `config/serve.json`            | Local server and debug-page configuration.                                                        |
| `config/rig.json`              | Points Heft to the standard `@microsoft/spfx-web-build-rig` configuration.                        |
| `sharepoint/assets/`           | Optional elements, schema, and upgrade XML used to provision SharePoint assets.                   |
| `sharepoint/solution/`         | Default output directory for the packaged `.sppkg` file.                                          |
| `src/webparts/`                | Client-side web part source, styles, localization, components, and manifest files.                |
| `src/extensions/`              | Application Customizer, Field Customizer, and Command Set source files.                           |
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

### Glossary

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

### FAQ and Troubleshooting

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

### Best Practices

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

## Official Docs & Resources

- [SharePoint Framework overview](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/sharepoint-framework-overview) - The official starting point for SPFx concepts, architecture, and capabilities.
- [SharePoint Framework compatibility matrix](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/compatibility) - Which SPFx version to use against SharePoint Online, Server 2019, and Subscription Edition.
- [SharePoint Framework extensions overview](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/extensions/overview-extensions) - Introduction to Application Customizers, Field Customizers, and Command Sets.
- [Set up your SharePoint Framework development environment](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-development-environment) - Official environment setup guide (Node.js, npm, tooling).
- [SharePoint Framework category — Microsoft 365 Developer Blog](https://devblogs.microsoft.com/microsoft365dev/category/sharepoint-framework/) - Official announcements, roadmap updates, and release notes.
- [Build your first SharePoint client-side web part (Hello World)](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/get-started/build-a-hello-world-web-part) - Microsoft's canonical step-by-step tutorial for scaffolding, previewing, and packaging a first web part.
- [SharePoint Framework Toolchain: Heft-based](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/toolchain/sharepoint-framework-toolchain-rushstack-heft) - Explains the Heft build toolchain that replaced gulp in SPFx v1.22, why it changed, and the migration timeline.
- [SharePoint Framework Debug Toolbar](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/debug-toolbar) - How to inspect and debug SPFx components on real modern pages, including extensions that the hosted workbench cannot test.
- [Connect SPFx components using dynamic data](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/dynamic-data) - Use dynamic data to connect web parts and other SPFx components on a page.
- [Use the MSGraphClientV3 to connect to Microsoft Graph](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/use-msgraph) - Authenticate and call Microsoft Graph through the SPFx context.
- [Accessibility in SharePoint web part design](https://learn.microsoft.com/en-us/sharepoint/dev/design/accessibility) - Design and test keyboard, screen-reader, and high-contrast experiences for web parts.

## Environment Setup Notes

- [Microsoft 365 Developer Program FAQ](https://learn.microsoft.com/en-us/office/developer-program/microsoft-365-developer-program-faq) - Check current eligibility for a free Microsoft 365 E5 developer sandbox; an ordinary Microsoft 365 enterprise subscription does not automatically include one.
- [Unavailable hosted workbench (Microsoft Community Hub thread)](https://techcommunity.microsoft.com/t5/sharepoint-developer/unavailable-hosted-workbench/td-p/3043377) - Background on why the fully local workbench (`https://localhost:4321/temp/workbench.html`, no SharePoint site needed) was removed starting with SPFx v1.13, and why the hosted workbench has required a tenant domain (via the `SPFX_SERVE_TENANT_DOMAIN` environment variable) since v1.17. If you have no tenant access at all, pin your project to SPFx v1.12.1 or earlier to keep a working local workbench.
- [🙏 Please upgrade React to a modern, supported version (SharePoint/sp-dev-docs#8265)](https://github.com/SharePoint/sp-dev-docs/issues/8265) - Context on why SPFx pins an exact React version per release (React 17.0.1 as of SPFx 1.19-1.23; see the official compatibility matrix above). Install React with `--save-exact` matching your SPFx version - mismatches fail silently at runtime instead of at build time.

## Getting Started / Generators

- [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint) - The official Yeoman generator for scaffolding SPFx web parts, extensions, and library components.
- [pnp/generator-spfx](https://github.com/pnp/generator-spfx) - Community-driven Yeoman generator that extends the official generator with extra governance options.
- [SharePoint/spfx](https://github.com/SharePoint/spfx) - Microsoft's new open-source `spfx` CLI and template system that is replacing the Yeoman-based generator.
- [spfx-fast-serve](https://github.com/s-KaiNet/spfx-fast-serve) - Faster local serving for legacy gulp-based SPFx projects; check support before using it with a Heft project.

## PnP Libraries

- [CLI for Microsoft 365](https://github.com/pnp/cli-microsoft365) - Cross-platform CLI to manage Microsoft 365 tenants and SPFx projects (validate, upgrade, deploy, and more).
- [PnPjs](https://github.com/pnp/pnpjs) - Fluent, modular JavaScript/TypeScript library for calling SharePoint and Microsoft Graph REST APIs.
- [PnP Modern Search](https://microsoft-search.github.io/pnp-modern-search/) - Open-source modern SharePoint web parts for building advanced search experiences in SharePoint Online.
- [PnP PowerShell](https://pnp.github.io/powershell/) - PowerShell cmdlets for common SharePoint Online provisioning, administration, and automation scenarios.
- [@pnp/spfx-controls-react](https://github.com/pnp/sp-dev-fx-controls-react) - Reusable React UI controls (people picker, rich text, list item picker, etc.) for SPFx web parts and extensions.
- [@pnp/spfx-property-controls](https://github.com/pnp/sp-dev-fx-property-controls) - Reusable property pane controls (site picker, collection data editor, and more) for SPFx web part properties.

## Sample Galleries

- [pnp/sp-dev-fx-extensions](https://github.com/pnp/sp-dev-fx-extensions) - Community sample gallery for SPFx Application Customizers, Field Customizers, and Command Sets.
- [pnp/sp-dev-fx-webparts](https://github.com/pnp/sp-dev-fx-webparts) - Community sample gallery of hundreds of SPFx web parts, Teams tabs, and personal apps.
- [OlivierCC/spfx-40-fantastics](https://github.com/OlivierCC/spfx-40-fantastics) - Sample kit of high-visual client-side web parts including carousels, image galleries, animations, maps, and editors.
- [pnp/sp-dev-fx-aces](https://github.com/pnp/sp-dev-fx-aces) - Community sample gallery of Adaptive Card Extensions (ACEs) for Microsoft Viva Connections dashboards.
- [React poll web part sample](https://github.com/pnp/sp-dev-fx-webparts/tree/main/samples/react-poll) - Inspect a complete React, PnPjs, and SharePoint-list example alongside the video tutorial below.

## Dev Tools & VS Code Extensions

- [Fluent UI Theme Designer](https://fluentuipr.z22.web.core.windows.net/heads/master/theming-designer/index.html) - Web-based designer for creating custom Fluent UI themes that can be applied to SPFx solutions.
- [SharePoint Framework Toolkit (vscode-viva)](https://github.com/pnp/vscode-viva) - VS Code extension covering the full SPFx lifecycle: scaffolding, samples, Gulp tasks, and tenant/app catalog management.
- [SP Editor](https://github.com/pnp/sp-editor) - Chrome/Edge browser extension for editing JS/CSS files, property bag values, and webhooks, and running PnP JS snippets directly against a SharePoint site from DevTools.
- [SP Formatter](https://marketplace.visualstudio.com/items?itemName=s-kainet.sp-formatter) - VS Code extension (paired with a browser extension) for editing SharePoint column, view, and form formatting JSON with IntelliSense and live preview.
- [SPFx Essentials](https://marketplace.visualstudio.com/items?itemName=eliostruyf.spfx-essentials) - VS Code extension with snippets and commands that speed up everyday SPFx project tasks.
- [Microsoft Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer) - Try Microsoft Graph requests and inspect responses before adding them to an SPFx component.
- [CLI for Microsoft 365: SPFx project doctor](https://pnp.github.io/cli-microsoft365/cmd/spfx/project/project-doctor/) - Check an SPFx project's dependencies and configuration and get a report of issues to fix.
- [CLI for Microsoft 365: SPFx project upgrade](https://pnp.github.io/cli-microsoft365/cmd/spfx/project/project-upgrade/) - Generate a version-specific upgrade report without changing project files.

## SharePoint Migration Tools

- [ShareGate](https://sharegate.com/download-migration-tool) - Microsoft 365 migration and governance tool that helps plan, move, and manage SharePoint content.
- [SharePoint Migration Tool](https://learn.microsoft.com/en-us/sharepointmigration/how-to-use-the-sharepoint-migration-tool) - Free Microsoft migration tool for moving content from on-premises SharePoint sites to Microsoft 365.

## Boilerplates & Starters

- [pnp/sp-starter-kit](https://github.com/pnp/sp-starter-kit) - Older end-to-end intranet showcase with SPFx web parts, extensions, and provisioning scripts; check its framework version before reusing code.
- [apvee/spfx-react-toolkit](https://github.com/apvee/spfx-react-toolkit) - React runtime and hooks library for SPFx with instance-scoped state isolation across web parts, extensions, and command sets.

## Testing & CI/CD

- [react-jest-testing sample](https://github.com/pnp/sp-dev-fx-webparts/tree/main/samples/react-jest-testing) - Official PnP sample showing Jest and Enzyme unit testing set up for an SPFx React web part.
- [pnp/action-cli-deploy](https://github.com/pnp/action-cli-deploy) - GitHub Action that deploys a packaged SPFx solution to a tenant or site app catalog using the CLI for Microsoft 365.
- [pnp/action-cli-login](https://github.com/pnp/action-cli-login) - GitHub Action that authenticates the CLI for Microsoft 365 inside a workflow, typically paired with `action-cli-deploy`.
- [Automate your CI/CD workflow using CLI for Microsoft 365 in GitHub Workflows](https://pnp.github.io/cli-microsoft365/user-guide/github-actions/) - Official guide to wiring the CLI for Microsoft 365 into GitHub Actions pipelines.
- [Implement CI/CD for SPFx with Azure Pipelines](https://github.com/SharePoint/sp-dev-docs/blob/main/docs/spfx/toolchain/implement-ci-cd-with-azure-pipelines.md) - Official Microsoft guidance for building and releasing SPFx solutions with Azure Pipelines.

## AI / Copilot Integrations

- [@spfx GitHub Copilot Chat participant](https://pnp.github.io/blog/post/spfx-toolkit-vscode-chat-pre-release/) - SPFx Toolkit's Copilot Chat participant that answers SPFx setup and scaffolding questions directly inside VS Code.
- [SPFx Toolkit Language Model Tools](https://pnp.github.io/vscode-viva/features/github-copilot-capabilities) - SPFx Toolkit's GitHub Copilot agent-mode tools for managing a SharePoint Online tenant (site creation, app catalog operations, page creation) directly from chat prompts.
- [pnp/cli-microsoft365-mcp-server](https://github.com/pnp/cli-microsoft365-mcp-server) - MCP server that exposes the CLI for Microsoft 365 as tools for AI agents to manage Microsoft 365 and SPFx projects.
- [Microsoft 365 Copilot extensibility overview](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/overview-copilot-connector) - Official docs on connecting Microsoft Graph data and custom connectors to Microsoft 365 Copilot.
- [SharePoint Framework (SPFx) roadmap update – July 2026](https://devblogs.microsoft.com/microsoft365dev/sharepoint-framework-spfx-roadmap-update-july-2026/) - Official roadmap post covering SharePoint Copilot Apps and upcoming AI-related SPFx capabilities.
- [Use GitHub Copilot to migrate SPFx 1.21 → 1.22 (Heft)](https://www.petkir.at/blog/spfx-1-22-copilot-assisted-migration) - Walkthrough with a reusable Copilot prompt for migrating an SPFx solution's toolchain from gulp to Heft.
- [SharePoint Copilot Apps overview (preview)](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/copilot/overview-copilot-apps) - Learn how SPFx components can provide interactive UI in Microsoft 365 Copilot during the public preview.
- [Build your first SharePoint Copilot App (preview)](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/copilot/get-started/build-your-first-copilot-app) - Create, test, package, and deploy a preview Copilot App with the official tutorial.

## Learning Resources

New to SPFx? Start with the development-environment module, build a web part, then learn SharePoint data and Microsoft Graph before packaging a solution for deployment. After that, follow the extensions or Viva Connections material for the component type you need. Check the official compatibility matrix above when a tutorial uses an older toolchain.

- [Voitanos blog (Andrew Connell)](https://www.andrewconnell.com/blog/) - Long-running, in-depth SPFx and Microsoft 365 development blog with courses and office hours.
- [PnP blog](https://pnp.github.io/blog/) - Official Microsoft 365 & Power Platform Community blog covering SPFx releases, tooling, and how-tos.
- [SharePoint Framework — Configure a development environment (Microsoft Learn training)](https://learn.microsoft.com/en-us/training/modules/sharepoint-spfx-get-started/) - Free, guided Microsoft Learn training module for getting started with SPFx.
- [Microsoft 365 & SharePoint PnP Weekly](https://www.youtube.com/playlist?list=PLB_fukFwGnsRCl_XIYjnJbMwOKlI9xkPK) - Long-running weekly video/podcast series covering SharePoint, SPFx, and Microsoft 365 dev news.
- [Use Microsoft Graph and non-Microsoft APIs (Microsoft Learn training)](https://learn.microsoft.com/en-us/training/modules/sharepoint-spfx-graph-3rd-party-apis/) - Intermediate hands-on module for anonymous REST APIs, Entra ID-protected APIs, and Microsoft Graph in SPFx.
- [Develop web parts with the SharePoint Framework (Microsoft Learn training)](https://learn.microsoft.com/en-us/training/modules/sharepoint-spfx-web-parts/) - Build and test client-side web parts in the SharePoint-hosted Workbench while exploring the core SPFx API.
- [Enable SharePoint Framework web part configuration with property panes (Microsoft Learn training)](https://learn.microsoft.com/en-us/training/modules/sharepoint-spfx-web-part-property-pane/) - Hands-on module for building property panes, custom field controls, and reusable PnP controls.
- [Work with SharePoint Content using the SharePoint Framework (Microsoft Learn training)](https://learn.microsoft.com/en-us/training/modules/sharepoint-spfx-spcontent/) - Practical module covering list and library CRUD, file uploads, mock data, and the SharePoint REST API.
- [Extend the SharePoint user interface with SharePoint Framework extensions (Microsoft Learn training)](https://learn.microsoft.com/en-us/training/modules/sharepoint-spfx-extensions/) - Build application customizers, field customizers, and command sets through guided exercises.
- [Build Microsoft Teams customization using the SharePoint Framework (Microsoft Learn training)](https://learn.microsoft.com/en-us/training/modules/sharepoint-spfx-teams-dev/) - Learn to surface SPFx web parts as Teams tabs and adapt components to their host.
- [Extend Microsoft SharePoint (Microsoft Learn learning path)](https://learn.microsoft.com/en-us/training/paths/m365-sharepoint-associate/) - Follow a nine-module path from environment setup through APIs, extensions, and production deployment.
- [Create Adaptive Card Extensions for Microsoft Viva Connections (Microsoft Learn training)](https://learn.microsoft.com/en-us/training/modules/sharepoint-spfx-adaptive-card-extension-card-types/) - Build card and quick views for Viva Connections dashboards in guided exercises.
- [Deploy SharePoint Framework components to production (Microsoft Learn training)](https://learn.microsoft.com/en-us/training/modules/sharepoint-spfx-deployment/) - Practice packaging, app-catalog deployment, and version updates.
- [Extend Microsoft Viva Connections (Microsoft Learn learning path)](https://learn.microsoft.com/en-us/training/paths/m365-extend-viva-connections/) - Learn when to use web parts, application customizers, and Adaptive Card Extensions in Viva Connections.
- [PnP SPFx sample getting-started guide](https://pnp.github.io/sp-dev-fx-webparts/gettingstarted/) - Find a sample's SPFx version, install its dependencies, and run it in a development tenant.
- [PnPjs getting started](https://pnp.github.io/pnpjs/getting-started/) - Set up PnPjs for SharePoint and Graph requests, including SPFx context integration and version requirements.

## Video Tutorials

> Treat these as onboarding material: they're great for learning how to scaffold a project, run it locally, and package/deploy it, but SPFx's APIs and best practices move fast enough that specific code shown in older videos can go stale within a year or two. Cross-check anything beyond the basics against the official docs linked above.

- [SharePoint Framework for Beginners, Series 2 (2025 playlist)](https://www.youtube.com/playlist?list=PLGWG_rRY_j4PxyQ3H9UMyECwvw3SWVMIK) - From-scratch lessons on environment setup, scaffolding, and React web parts; compare toolchain steps with the current docs.
- [SPGuides YouTube channel](https://www.youtube.com/channel/UCm9EZ5sUkwJCbA3ctabVQJg) - Large, frequently updated library of SPFx, SharePoint, and Power Platform video tutorials from Microsoft MVP Bijay Kumar.
- [Mastering the SharePoint Framework (Voitanos)](https://www.voitanos.io/course-master-sharepoint-framework/) - Paid, in-depth video course by Andrew Connell covering SPFx fundamentals through advanced extensibility topics.
- [SharePoint Framework: Getting started with extending the UX (Microsoft Community Learning)](https://www.youtube.com/watch?v=kNFi4H84Uds) - Overview of where SPFx web parts and extensions fit across Microsoft 365.
- [Introducing the new toolchain in SharePoint Framework 1.22 (Microsoft Community Learning)](https://www.youtube.com/watch?v=VlQgS9ldc3Y) - Walkthrough of the Heft-based build workflow with Vesa Juvonen and Andrew Connell.
- [Getting Started with SPFx Application Customizer (Microsoft Community Learning)](https://www.youtube.com/watch?v=HTrr1YfP1U8) - Beginner-friendly demonstration of an Application Customizer extension.
- [Building a React Calendar Web Part with SPFx (Microsoft Community Learning)](https://www.youtube.com/watch?v=39jRwZHg698) - Practical React web-part sample; check its SPFx version before copying dependencies.
- [Building a custom poll web part with SPFx and React (Microsoft Community Learning)](https://www.youtube.com/watch?v=BoiNdY97AV0) - Follow a React Hooks and PnPjs build with a linked source sample and SharePoint list provisioning.
- [Adaptive Card Extensions for Viva Connections (Microsoft Community Learning playlist)](https://www.youtube.com/playlist?list=PLR9nK3mnD-OUjNKUMsWJwYnRnsmxXojYs) - Card and quick-view walkthroughs recorded with an older SPFx toolchain; use current docs for setup commands.
- [Creating your first SharePoint Copilot App (Microsoft Community Learning)](https://www.youtube.com/watch?v=1TaK6osdvc0) - End-to-end preview tutorial for an SPFx Copilot App; follow the preview documentation for current requirements.

## Community

- [SharePoint Developer Community resources (Microsoft Learn)](https://learn.microsoft.com/en-us/sharepoint/dev/community/community) - Official index of PnP community calls, blogs, and GitHub organizations.
- [SharePoint Stack Exchange — sharepoint-framework tag](https://sharepoint.stackexchange.com/questions/tagged/sharepoint-framework) - Q&A tag for SharePoint Framework development questions.
- [Microsoft 365 & Power Platform Community calls](https://aka.ms/community/calls) - Weekly community calls covering Microsoft 365, Power Platform, and SPFx news, demos, and Q&A.
- [Microsoft 365 and SharePoint Server Discord](https://discord.com/invite/r-sharepoint-874829774902689863) - Community Discord server for SharePoint, Microsoft 365, and SPFx discussion.
- [Microsoft 365 & Power Platform Community (PnP)](https://pnp.github.io/) - Community-driven guidance, documentation, samples, and tooling for modern SharePoint and Microsoft 365 development.
- [PnP GitHub organization](https://github.com/pnp) - Home of the official and community-maintained PnP repositories referenced throughout this list.

## Contributing

Contributions are welcome! Please read the [contribution guidelines](CONTRIBUTING.md) first.
