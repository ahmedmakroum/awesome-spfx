# Awesome SPFx [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of resources, libraries, tools, and community content for building SharePoint Framework (SPFx) solutions.

The **SharePoint Framework (SPFx)** is Microsoft's page and web part development model for building client-side web parts, extensions, and Adaptive Card Extensions that run in SharePoint, Microsoft Teams, Outlook, and Viva Connections. It's built on modern web tooling (TypeScript, npm, Webpack) and is the recommended way to extend SharePoint and Microsoft 365 with custom UI.

This list is for developers who are new to SPFx and want a map of the ecosystem, as well as experienced developers looking for well-maintained libraries, tools, and community resources.

There isn't a lot of curated, up-to-date documentation specifically for the SPFx ecosystem, most resources are scattered across official docs, blogs, and GitHub repos. I decided to put this list together to bring them into one place and hopefully save others some digging. I maintain a few other projects and write about web development from time to time, feel free to check out my [GitHub profile](https://github.com/ahmedmakroum) if you're curious.

## Contents

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

## Official Docs & Resources

- [SharePoint Framework overview](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/sharepoint-framework-overview) - The official starting point for SPFx concepts, architecture, and capabilities.
- [SharePoint Framework compatibility matrix](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/compatibility) - Which SPFx version to use against SharePoint Online, Server 2019, and Subscription Edition.
- [SharePoint Framework extensions overview](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/extensions/overview-extensions) - Introduction to Application Customizers, Field Customizers, and Command Sets.
- [Set up your SharePoint Framework development environment](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-development-environment) - Official environment setup guide (Node.js, npm, tooling).
- [SharePoint Framework category — Microsoft 365 Developer Blog](https://devblogs.microsoft.com/microsoft365dev/category/sharepoint-framework/) - Official announcements, roadmap updates, and release notes.

## Environment Setup Notes

- [Microsoft 365 Developer Program FAQ](https://learn.microsoft.com/en-us/office/developer-program/microsoft-365-developer-program-faq) - Microsoft paused issuing free instant sandbox tenants after a January 2024 security incident and still hasn't fully restored them. In practice, plan on using your company/work tenant, converting a purchased Microsoft 365 subscription into a dev tenant, or qualifying through a Visual Studio subscription.
- [Unavailable hosted workbench (Microsoft Community Hub thread)](https://techcommunity.microsoft.com/t5/sharepoint-developer/unavailable-hosted-workbench/td-p/3043377) - Background on why the fully local workbench (`https://localhost:4321/temp/workbench.html`, no SharePoint site needed) was removed starting with SPFx v1.13, and why the hosted workbench has required a tenant domain (via the `SPFX_SERVE_TENANT_DOMAIN` environment variable) since v1.17. If you have no tenant access at all, pin your project to SPFx v1.12.1 or earlier to keep a working local workbench.
- [🙏 Please upgrade React to a modern, supported version (SharePoint/sp-dev-docs#8265)](https://github.com/SharePoint/sp-dev-docs/issues/8265) - Context on why SPFx pins an exact React version per release (React 17.0.1 as of SPFx 1.19-1.23, see the [compatibility matrix](#official-docs--resources)). Install React with `--save-exact` matching your SPFx version - mismatches fail silently at runtime instead of at build time.

## Getting Started / Generators

- [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint) - The official Yeoman generator for scaffolding SPFx web parts, extensions, and library components.
- [pnp/generator-spfx](https://github.com/pnp/generator-spfx) - Community-driven Yeoman generator that extends the official generator with extra governance options.
- [SharePoint/spfx](https://github.com/SharePoint/spfx) - Microsoft's new open-source `spfx` CLI and template system that is replacing the Yeoman-based generator.
- [spfx-fast-serve](https://github.com/s-KaiNet/spfx-fast-serve) - Drop-in Webpack-based dev server that makes `gulp serve` 10-15x faster.

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

## Dev Tools & VS Code Extensions

- [Fluent UI Theme Designer](https://fluentuipr.z22.web.core.windows.net/heads/master/theming-designer/index.html) - Web-based designer for creating custom Fluent UI themes that can be applied to SPFx solutions.
- [SharePoint Framework Toolkit (vscode-viva)](https://github.com/pnp/vscode-viva) - VS Code extension covering the full SPFx lifecycle: scaffolding, samples, Gulp tasks, and tenant/app catalog management.
- [SP Editor](https://github.com/pnp/sp-editor) - Chrome/Edge browser extension for editing JS/CSS files, property bag values, and webhooks, and running PnP JS snippets directly against a SharePoint site from DevTools.
- [SP Formatter](https://marketplace.visualstudio.com/items?itemName=s-kainet.sp-formatter) - VS Code extension (paired with a browser extension) for editing SharePoint column, view, and form formatting JSON with IntelliSense and live preview.
- [SPFx Essentials](https://marketplace.visualstudio.com/items?itemName=eliostruyf.spfx-essentials) - VS Code extension with snippets and commands that speed up everyday SPFx project tasks.

## SharePoint Migration Tools

- [ShareGate](https://sharegate.com/download-migration-tool) - Microsoft 365 migration and governance tool that helps plan, move, and manage SharePoint content.
- [SharePoint Migration Tool](https://learn.microsoft.com/en-us/sharepointmigration/how-to-use-the-sharepoint-migration-tool) - Free Microsoft migration tool for moving content from on-premises SharePoint sites to Microsoft 365.

## Boilerplates & Starters

- [pnp/sp-starter-kit](https://github.com/pnp/sp-starter-kit) - End-to-end showcase solution bundling multiple SPFx web parts, extensions, and provisioning scripts to jump-start a modern intranet.
- [apvee/spfx-react-toolkit](https://github.com/apvee/spfx-react-toolkit) - React runtime and hooks library for SPFx with instance-scoped state isolation across web parts, extensions, and command sets.

## Testing & CI/CD

- [react-jest-testing sample](https://github.com/pnp/sp-dev-fx-webparts/tree/main/samples/react-jest-testing) - Official PnP sample showing Jest and Enzyme unit testing set up for an SPFx React web part.
- [pnp/action-cli-deploy](https://github.com/pnp/action-cli-deploy) - GitHub Action that deploys a packaged SPFx solution to a tenant or site app catalog using the CLI for Microsoft 365.
- [pnp/action-cli-login](https://github.com/pnp/action-cli-login) - GitHub Action that authenticates the CLI for Microsoft 365 inside a workflow, typically paired with `action-cli-deploy`.
- [Automate your CI/CD workflow using CLI for Microsoft 365 in GitHub Workflows](https://pnp.github.io/cli-microsoft365/user-guide/github-actions/) - Official guide to wiring the CLI for Microsoft 365 into GitHub Actions pipelines.
- [Implement CI/CD for SPFx with Azure Pipelines](https://github.com/SharePoint/sp-dev-docs/blob/main/docs/spfx/toolchain/implement-ci-cd-with-azure-pipelines.md) - Official Microsoft guidance for building and releasing SPFx solutions with Azure Pipelines.

## AI / Copilot Integrations

> **From experience:** for day-to-day SPFx development, ChatGPT Codex has felt noticeably more effective than Claude - it seems to hold SPFx-specific context (manifests, gulp/Heft toolchain quirks, PnP API shapes) better across a session and needs less hand-holding. This is a personal, anecdotal observation rather than a benchmark, so your mileage may vary depending on the task.

- [@spfx GitHub Copilot Chat participant](https://pnp.github.io/blog/post/spfx-toolkit-vscode-chat-pre-release/) - SPFx Toolkit's Copilot Chat participant that answers SPFx setup and scaffolding questions directly inside VS Code.
- [SPFx Toolkit Language Model Tools](https://pnp.github.io/vscode-viva/features/github-copilot-capabilities) - SPFx Toolkit's GitHub Copilot agent-mode tools for managing a SharePoint Online tenant (site creation, app catalog operations, page creation) directly from chat prompts.
- [pnp/cli-microsoft365-mcp-server](https://github.com/pnp/cli-microsoft365-mcp-server) - MCP server that exposes the CLI for Microsoft 365 as tools for AI agents to manage Microsoft 365 and SPFx projects.
- [Microsoft 365 Copilot extensibility overview](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/overview-copilot-connector) - Official docs on connecting Microsoft Graph data and custom connectors to Microsoft 365 Copilot.
- [SharePoint Framework (SPFx) roadmap update – July 2026](https://devblogs.microsoft.com/microsoft365dev/sharepoint-framework-spfx-roadmap-update-july-2026/) - Official roadmap post covering SharePoint Copilot Apps and upcoming AI-related SPFx capabilities.
- [Use GitHub Copilot to migrate SPFx 1.21 → 1.22 (Heft)](https://www.petkir.at/blog/spfx-1-22-copilot-assisted-migration) - Walkthrough with a reusable Copilot prompt for migrating an SPFx solution's toolchain from gulp to Heft.

## Learning Resources

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

## Video Tutorials

> Treat these as onboarding material: they're great for learning how to scaffold a project, run it locally, and package/deploy it, but SPFx's APIs and best practices move fast enough that specific code shown in older videos can go stale within a year or two. Cross-check anything beyond the basics against the official docs linked above.

- [SharePoint Framework for Beginners 2025 (playlist)](https://www.youtube.com/watch?v=tL-qXVMDtFk) - Actively updated, from-scratch series covering environment setup, Yeoman scaffolding, and building web parts with React hooks.
- [SPGuides YouTube channel](https://www.youtube.com/channel/UCm9EZ5sUkwJCbA3ctabVQJg) - Large, frequently updated library of SPFx, SharePoint, and Power Platform video tutorials from Microsoft MVP Bijay Kumar.
- [Mastering the SharePoint Framework (Voitanos)](https://www.voitanos.io/course-master-sharepoint-framework/) - Paid, in-depth video course by Andrew Connell covering SPFx fundamentals through advanced extensibility topics.

## Community

- [SharePoint Developer Community resources (Microsoft Learn)](https://learn.microsoft.com/en-us/sharepoint/dev/community/community) - Official index of PnP community calls, blogs, and GitHub organizations.
- [SharePoint Stack Exchange — sharepoint-framework tag](https://sharepoint.stackexchange.com/questions/tagged/sharepoint-framework) - Q&A tag for SharePoint Framework development questions.
- [Microsoft 365 & Power Platform Community calls](https://aka.ms/community/calls) - Weekly community calls covering Microsoft 365, Power Platform, and SPFx news, demos, and Q&A.
- [Microsoft 365 and SharePoint Server Discord](https://discord.com/invite/r-sharepoint-874829774902689863) - Community Discord server for SharePoint, Microsoft 365, and SPFx discussion.
- [Microsoft 365 & Power Platform Community (PnP)](https://pnp.github.io/) - Community-driven guidance, documentation, samples, and tooling for modern SharePoint and Microsoft 365 development.
- [PnP GitHub organization](https://github.com/pnp) - Home of the official and community-maintained PnP repositories referenced throughout this list.

## Contributing

Contributions are welcome! Please read the [contribution guidelines](CONTRIBUTING.md) first.
