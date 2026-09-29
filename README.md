# Awesome SPFx [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Client-side development framework for extending SharePoint, Microsoft Teams, Outlook, and Viva Connections with web parts, extensions, and Adaptive Card Extensions.

The [SharePoint Framework (SPFx)](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/sharepoint-framework-overview) uses TypeScript and modern web tooling to build Microsoft 365 experiences. This list brings together documentation, training, libraries, samples, and practical development guidance.

## Contents

- [Official Documentation](#official-documentation)
- [Learning Resources](#learning-resources)
  - [JavaScript, TypeScript, and React](#javascript-typescript-and-react)
  - [Guided SPFx Training](#guided-spfx-training)
  - [Sample Walkthroughs and Blogs](#sample-walkthroughs-and-blogs)
- [Environment Setup](#environment-setup)
- [Generators and Build Tools](#generators-and-build-tools)
- [Libraries and Reusable Controls](#libraries-and-reusable-controls)
- [Sample Galleries](#sample-galleries)
- [Developer Tools](#developer-tools)
- [Data Access and APIs](#data-access-and-apis)
- [UI, Accessibility, and Localization](#ui-accessibility-and-localization)
- [Extensions and Viva Connections](#extensions-and-viva-connections)
- [Performance](#performance)
- [Security and Deployment](#security-and-deployment)
- [Testing and CI/CD](#testing-and-cicd)
- [Migration and Upgrades](#migration-and-upgrades)
- [AI and Copilot Integrations](#ai-and-copilot-integrations)
- [Video Tutorials](#video-tutorials)
- [Community](#community)
- [Tips and Tricks](#tips-and-tricks)

## Official Documentation

- [SharePoint Framework compatibility matrix](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/compatibility) - Which SPFx version to use against SharePoint Online, Server 2019, and Subscription Edition.
- [Set up your SharePoint Framework development environment](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-development-environment) - Official environment setup guide (Node.js, npm, tooling).
- [SharePoint Framework category — Microsoft 365 Developer Blog](https://devblogs.microsoft.com/microsoft365dev/category/sharepoint-framework/) - Official announcements, roadmap updates, and release notes.
- [SharePoint Framework Toolchain: Heft-based](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/toolchain/sharepoint-framework-toolchain-rushstack-heft) - Explains the Heft build toolchain that replaced gulp in SPFx v1.22, why it changed, and the migration timeline.
- [SharePoint Framework API reference](https://learn.microsoft.com/en-us/javascript/api/overview/sharepoint?view=sp-typescript-latest) - TypeScript reference for framework classes, services, context objects, and component APIs.

## Learning Resources

Start with the [guided learning path and practice projects](docs/tips-and-tricks.md#learning-path). Training and videos can use older dependencies or gulp commands; match their concepts to your project's SPFx version using the official documentation above.

### JavaScript, TypeScript, and React

- [MDN asynchronous JavaScript](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Async_JS) - Learn promises, async/await, and error handling before connecting components to remote APIs.
- [React Learn](https://react.dev/learn) - Learn components, props, state, and hooks; check SPFx's supported React version before adopting newer APIs or installation instructions.
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html) - Understand interfaces, unions, generics, and narrowing for typed web-part properties and service responses.

### Guided SPFx Training

- [SharePoint Framework — Configure a development environment (Microsoft Learn training)](https://learn.microsoft.com/en-us/training/modules/sharepoint-spfx-get-started/) - Free, guided Microsoft Learn training module for getting started with SPFx.
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
- [Build your first SharePoint client-side web part (Hello World)](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/get-started/build-a-hello-world-web-part) - Microsoft's canonical step-by-step tutorial for scaffolding, previewing, and packaging a first web part.

### Sample Walkthroughs and Blogs

- [Voitanos blog (Andrew Connell)](https://www.andrewconnell.com/blog/) - Long-running, in-depth SPFx and Microsoft 365 development blog with courses and office hours.
- [PnP blog](https://pnp.github.io/blog/) - Official Microsoft 365 & Power Platform Community blog covering SPFx releases, tooling, and how-tos.
- [PnP SPFx sample getting-started guide](https://pnp.github.io/sp-dev-fx-webparts/gettingstarted/) - Find a sample's SPFx version, install its dependencies, and run it in a development tenant.
- [Mastering the SharePoint Framework (Voitanos)](https://www.voitanos.io/course-master-sharepoint-framework/) - Paid, in-depth video course by Andrew Connell covering SPFx fundamentals through advanced extensibility topics.


## Environment Setup

- [Microsoft 365 Developer Program FAQ](https://learn.microsoft.com/en-us/office/developer-program/microsoft-365-developer-program-faq) - Check current eligibility for a free Microsoft 365 E5 developer sandbox; an ordinary Microsoft 365 enterprise subscription does not automatically include one.
- [Set up a Microsoft 365 development tenant](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-developer-tenant) - Prepare an app catalog and development site for testing SPFx components.
- [Hosted workbench transition](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/release-1.13.0) - Explains removal of the local workbench in SPFx 1.13; use a development tenant for current SPFx projects.
- [React version compatibility discussion](https://github.com/SharePoint/sp-dev-docs/issues/8265) - Maintainer discussion of React support; use the official compatibility matrix for the exact version supported by your SPFx release.

## Generators and Build Tools

- [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint) - The official Yeoman generator for scaffolding SPFx web parts, extensions, and library components.
- [pnp/generator-spfx](https://github.com/pnp/generator-spfx) - Community-driven Yeoman generator that extends the official generator with extra governance options.
- [spfx-fast-serve](https://github.com/s-KaiNet/spfx-fast-serve) - Faster local serving for legacy gulp-based SPFx projects; check support before using it with a Heft project.
- [SharePoint SPFx CLI](https://github.com/SharePoint/spfx) - Pre-release Microsoft CLI and versioned templates for scaffolding SPFx components; APIs and commands may change.
- [Understanding the Heft-based toolchain](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/toolchain/customize-heft-toolchain-overview) - Learn how rigs, build phases, plugins, and configuration fit together in SPFx.

## Libraries and Reusable Controls

- [CLI for Microsoft 365](https://github.com/pnp/cli-microsoft365) - Cross-platform CLI to manage Microsoft 365 tenants and SPFx projects (validate, upgrade, deploy, and more).
- [PnPjs](https://github.com/pnp/pnpjs) - Fluent, modular JavaScript/TypeScript library for calling SharePoint and Microsoft Graph REST APIs.
- [PnP Modern Search](https://microsoft-search.github.io/pnp-modern-search/) - Open-source modern SharePoint web parts for building advanced search experiences in SharePoint Online.
- [PnP PowerShell](https://pnp.github.io/powershell/) - PowerShell cmdlets for common SharePoint Online provisioning, administration, and automation scenarios.
- [@pnp/spfx-controls-react](https://github.com/pnp/sp-dev-fx-controls-react) - Reusable React UI controls (people picker, rich text, list item picker, etc.) for SPFx web parts and extensions.
- [@pnp/spfx-property-controls](https://github.com/pnp/sp-dev-fx-property-controls) - Reusable property pane controls (site picker, collection data editor, and more) for SPFx web part properties.
- [apvee/spfx-react-toolkit](https://github.com/apvee/spfx-react-toolkit) - React runtime and hooks library for SPFx with instance-scoped state isolation across web parts, extensions, and command sets.

## Sample Galleries

- [SPFx Library by Ahmed Makroum](https://github.com/ahmedmakroum/spfx-library) - SPFx web-part collection covering list analytics, approvals, project health, employee onboarding, and knowledge discovery, with mock-data demos for learning and adaptation.
- [Microsoft 365 Sample Solution Gallery](https://adoption.microsoft.com/en-us/sample-solution-gallery/) - Discover community solutions across Microsoft 365 and filter for SharePoint Framework scenarios.
- [pnp/sp-dev-fx-extensions](https://github.com/pnp/sp-dev-fx-extensions) - Community sample gallery for SPFx Application Customizers, Field Customizers, and Command Sets.
- [pnp/sp-dev-fx-webparts](https://github.com/pnp/sp-dev-fx-webparts) - Community sample gallery of hundreds of SPFx web parts, Teams tabs, and personal apps.
- [pnp/sp-dev-fx-aces](https://github.com/pnp/sp-dev-fx-aces) - Community sample gallery of Adaptive Card Extensions (ACEs) for Microsoft Viva Connections dashboards.
- [React poll web part sample](https://github.com/pnp/sp-dev-fx-webparts/tree/main/samples/react-poll) - Inspect a complete React, PnPjs, and SharePoint-list example alongside the video tutorial below.

## Developer Tools

- [Fluent UI Theme Designer](https://fluentuipr.z22.web.core.windows.net/heads/master/theming-designer/index.html) - Web-based designer for creating custom Fluent UI themes that can be applied to SPFx solutions.
- [SharePoint Framework Toolkit (vscode-viva)](https://github.com/pnp/vscode-viva) - VS Code extension covering the SPFx development workflow, including scaffolding, samples, local development, and app catalog management.
- [SP Editor](https://github.com/pnp/sp-editor) - Chrome/Edge browser extension for editing JS/CSS files, property bag values, and webhooks, and running PnP JS snippets directly against a SharePoint site from DevTools.
- [SP Formatter](https://marketplace.visualstudio.com/items?itemName=s-kainet.sp-formatter) - VS Code extension (paired with a browser extension) for editing SharePoint column, view, and form formatting JSON with IntelliSense and live preview.
- [SPFx Essentials](https://marketplace.visualstudio.com/items?itemName=eliostruyf.spfx-essentials) - VS Code extension with snippets and commands that speed up everyday SPFx project tasks.
- [Microsoft Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer) - Try Microsoft Graph requests and inspect responses before adding them to an SPFx component.
- [CLI for Microsoft 365: SPFx project doctor](https://pnp.github.io/cli-microsoft365/cmd/spfx/project/project-doctor/) - Check an SPFx project's dependencies and configuration and get a report of issues to fix.
- [CLI for Microsoft 365: SPFx project upgrade](https://pnp.github.io/cli-microsoft365/cmd/spfx/project/project-upgrade/) - Generate a version-specific upgrade report and migration scripts to review before applying changes.
- [SharePoint Framework Debug Toolbar](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/debug-toolbar) - How to inspect and debug SPFx components on real modern pages, including extensions that the hosted workbench cannot test.

## Data Access and APIs

- [Use the MSGraphClientV3 to connect to Microsoft Graph](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/use-msgraph) - Authenticate and call Microsoft Graph through the SPFx context.
- [PnPjs getting started](https://pnp.github.io/pnpjs/getting-started/) - Set up PnPjs for SharePoint and Graph requests, including SPFx context integration and version requirements.
- [PnPjs in SPFx](https://pnp.github.io/pnpjs/concepts/auth-spfx/) - Configure SharePoint and Graph clients with the SPFx context and authentication behaviors.
- [PnPjs batching](https://pnp.github.io/pnpjs/concepts/batching/) - Queue and execute multiple SharePoint or Graph requests while understanding batch lifecycle and request ordering.
- [Connect to Microsoft Entra ID-secured APIs](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/use-aadhttpclient) - Use AadHttpClient, declare API permission requests, and understand administrator approval.
- [Microsoft Graph throttling guidance](https://learn.microsoft.com/en-us/graph/throttling) - Handle throttled requests with Retry-After and retry policies, including failures inside batch responses.

## UI, Accessibility, and Localization

- [Accessibility in SharePoint web part design](https://learn.microsoft.com/en-us/sharepoint/dev/design/accessibility) - Design and test keyboard, screen-reader, and high-contrast experiences for web parts.
- [ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/) - Keyboard interaction and accessibility patterns for dialogs, tabs, menus, and other custom controls.
- [CSS recommendations for SPFx](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/css-recommendations) - Scope styles to components and avoid depending on SharePoint's internal DOM or CSS classes.
- [Support section backgrounds](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/guidance/supporting-section-backgrounds) - Make web parts theme-aware with theme variants and the ThemeProvider service.
- [Localize client-side web parts](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/guidance/localize-web-parts) - Organize translated strings and test localized web-part experiences.
- [Cascading property-pane dropdowns](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/guidance/use-cascading-dropdowns-in-web-part-properties) - Load dependent configuration choices, such as selecting a list before selecting a field.
- [Integrate web-part properties with SharePoint](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/guidance/integrate-web-part-properties-with-sharepoint) - Describe text, links, and HTML properties so SharePoint can process them appropriately.

## Extensions and Viva Connections

- [SharePoint Framework extensions overview](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/extensions/overview-extensions) - Overview of extension types and supported customization points.
- [Application Customizer placeholders](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/extensions/get-started/using-page-placeholder-with-extensions) - Render into supported page placeholders and respond when placeholder availability changes.
- [Build a Form Customizer](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/extensions/get-started/building-form-customizer) - Replace list forms with custom new, edit, and display experiences.
- [Build an Adaptive Card Extension](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/viva/get-started/build-first-sharepoint-adaptive-card-extension) - Create card and quick views and explore the ACE development lifecycle.
- [Connect SPFx components using dynamic data](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/dynamic-data) - Use dynamic data to connect web parts and other SPFx components on a page.

## Performance

- [Dynamic loading of packages](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/dynamic-loading) - Split large bundles and defer optional features or property-pane resources until they are needed.
- [PnPjs caching behaviors](https://pnp.github.io/pnpjs/queryable/behaviors/) - Configure caching and request behaviors, including expiration and opt-out options.
- [SharePoint performance guidance](https://learn.microsoft.com/en-us/sharepoint/dev/scenario-guidance/performance) - Understand client rendering, request volume, caching, and throttling considerations.

## Security and Deployment

- [SPFx enterprise guidance](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/enterprise-guidance) - Understand runtime trust, permissions, deployment, and organizational considerations.
- [Content Security Policy in SharePoint Online](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/content-securty-policy-trusted-script-sources) - Understand trusted script sources and prepare customizations for SharePoint's CSP requirements.
- [Solution governance considerations](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/guidance/governance-considerations) - Review solution packages, hosted assets, and the impact of deploying custom code.
- [Tenant-scoped deployment](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/tenant-scoped-deployment) - Understand skipFeatureDeployment, tenant-wide availability, and limitations on provisioning assets.
- [Site collection app catalogs](https://learn.microsoft.com/en-us/sharepoint/dev/general-development/site-collection-app-catalog) - Distribute solutions within a specific site collection and understand administrative prerequisites.

## Testing and CI/CD

- [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/) - Test components through user-visible behavior; select a library version compatible with your SPFx React version.
- [Playwright](https://playwright.dev/docs/intro) - Automate browser tests for deployed web parts and extensions in a development tenant.
- [Accessibility testing with Playwright](https://playwright.dev/docs/accessibility-testing) - Add axe-based accessibility checks alongside manual keyboard and screen-reader testing.
- [pnp/action-cli-deploy](https://github.com/pnp/action-cli-deploy) - GitHub Action that deploys a packaged SPFx solution to a tenant or site app catalog using the CLI for Microsoft 365.
- [pnp/action-cli-login](https://github.com/pnp/action-cli-login) - GitHub Action that authenticates the CLI for Microsoft 365 inside a workflow, typically paired with `action-cli-deploy`.
- [Automate your CI/CD workflow using CLI for Microsoft 365 in GitHub Workflows](https://pnp.github.io/cli-microsoft365/user-guide/github-actions/) - Official guide to wiring the CLI for Microsoft 365 into GitHub Actions pipelines.
- [Implement CI/CD for SPFx with Azure Pipelines](https://github.com/SharePoint/sp-dev-docs/blob/main/docs/spfx/toolchain/implement-ci-cd-with-azure-pipelines.md) - Official Microsoft guidance for building and releasing SPFx solutions with Azure Pipelines.

## Migration and Upgrades

- [Migrate from gulp to Heft](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/toolchain/migrate-gulptoolchain-hefttoolchain) - Use the CLI for Microsoft 365 upgrade report to review dependency, configuration, and build-script changes.
- [Transform SharePoint-hosted Add-ins into SPFx solutions](https://learn.microsoft.com/en-us/sharepoint/dev/sp-add-ins-modernize/from-sharepoint-hosted-to-client-side) - Map older SharePoint-hosted customizations to client-side components and modern API access.
- [Domain-isolated web-part retirement](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/isolated-web-parts-retirement) - Find affected solutions and review migration steps following the April 2, 2026 retirement.

## AI and Copilot Integrations

- [@spfx GitHub Copilot Chat participant](https://pnp.github.io/blog/post/spfx-toolkit-vscode-chat-pre-release/) - SPFx Toolkit's Copilot Chat participant that answers SPFx setup and scaffolding questions directly inside VS Code.
- [SPFx Toolkit Language Model Tools](https://pnp.github.io/vscode-viva/features/github-copilot-capabilities) - SPFx Toolkit's GitHub Copilot agent-mode tools for managing a SharePoint Online tenant (site creation, app catalog operations, page creation) directly from chat prompts.
- [pnp/cli-microsoft365-mcp-server](https://github.com/pnp/cli-microsoft365-mcp-server) - MCP server that exposes the CLI for Microsoft 365 as tools for AI agents to manage Microsoft 365 and SPFx projects.
- [Microsoft 365 Copilot extensibility overview](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/overview-copilot-connector) - Official docs on connecting Microsoft Graph data and custom connectors to Microsoft 365 Copilot.
- [SharePoint Framework (SPFx) roadmap update – July 2026](https://devblogs.microsoft.com/microsoft365dev/sharepoint-framework-spfx-roadmap-update-july-2026/) - Official roadmap post covering SharePoint Copilot Apps and upcoming AI-related SPFx capabilities.
- [Use GitHub Copilot to migrate SPFx 1.21 → 1.22 (Heft)](https://www.petkir.at/blog/spfx-1-22-copilot-assisted-migration) - Walkthrough with a reusable Copilot prompt for migrating an SPFx solution's toolchain from gulp to Heft.
- [SharePoint Copilot Apps overview (preview)](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/copilot/overview-copilot-apps) - Learn how SPFx components can provide interactive UI in Microsoft 365 Copilot during the public preview.
- [Build your first SharePoint Copilot App (preview)](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/copilot/get-started/build-your-first-copilot-app) - Create, test, package, and deploy a preview Copilot App with the official tutorial.

## Video Tutorials

Check the recording date and sample dependencies before following setup commands. Preview demonstrations require the corresponding preview documentation.

- [Microsoft 365 & SharePoint PnP Weekly](https://www.youtube.com/playlist?list=PLB_fukFwGnsRCl_XIYjnJbMwOKlI9xkPK) - Long-running weekly video/podcast series covering SharePoint, SPFx, and Microsoft 365 dev news.
- [SharePoint Framework for Beginners, Series 2 (2025 playlist)](https://www.youtube.com/playlist?list=PLGWG_rRY_j4PxyQ3H9UMyECwvw3SWVMIK) - From-scratch lessons on environment setup, scaffolding, and React web parts; compare toolchain steps with the current docs.
- [SPGuides YouTube channel](https://www.youtube.com/channel/UCm9EZ5sUkwJCbA3ctabVQJg) - Large, frequently updated library of SPFx, SharePoint, and Power Platform video tutorials from Microsoft MVP Bijay Kumar.
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

## Tips and Tricks

The [SPFx quick reference](docs/quick-reference.md) covers setup steps, Heft and gulp commands, project layout, context APIs, troubleshooting, and best practices.

The [practical tips and learning projects](docs/tips-and-tricks.md) guide adds a learning sequence, batching and caching pitfalls, debugging habits, release checks, and six practice projects.

## Contributing

Contributions are welcome! Please read the [contribution guidelines](CONTRIBUTING.md) first.

## Footnotes

For older samples and adjacent content-migration tools, see the [historical and migration resources](docs/historical-resources.md).
