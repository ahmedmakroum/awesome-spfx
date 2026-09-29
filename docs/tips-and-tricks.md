# SPFx Tips and Tricks

[Back to Awesome SPFx](../README.md) · [Command quick reference](quick-reference.md)

These notes complement the resource directory with a learning sequence and practical habits. Follow your project's SPFx compatibility requirements when adapting a sample.

## Contents

- [Learning Path](#learning-path)
- [Environment and Debugging](#environment-and-debugging)
- [Data Access](#data-access)
- [Rendering and Performance](#rendering-and-performance)
- [UI and Component Lifecycle](#ui-and-component-lifecycle)
- [Release Checklist](#release-checklist)
- [Practice Projects](#practice-projects)

## Learning Path

Work through the [guided SPFx training](../README.md#guided-spfx-training) in this order. Move on when you can complete the outcome without copying the entire tutorial.

| Stage | Focus | Outcome |
| --- | --- | --- |
| 1. Foundations | TypeScript interfaces, React props and state, promises, and async/await. | Build a small typed component with loading and error states. |
| 2. First web part | Tenant setup, supported Node.js, generator, local HTTPS, and hosted workbench. | Render a web part on a real development-site page. |
| 3. Configuration | Property panes, validation, and dependent fields. | Let an author choose a list and fields without editing code. |
| 4. Data access | SharePoint REST or PnPjs, Graph clients, permissions, and pagination. | Load only the required data and explain permission failures. |
| 5. Production quality | Theming, accessibility, localization, and component cleanup. | Test two instances on one page, keyboard navigation, and another theme. |
| 6. Deployment | Production packaging, app catalogs, API approval, and version updates. | Install a package and test an upgrade on a development site. |
| 7. Specialization | Extensions, Teams hosting, or Adaptive Card Extensions. | Build a component for the host and workflow you actually need. |

The [JavaScript, TypeScript, and React resources](../README.md#javascript-typescript-and-react) cover prerequisites. Use the [sample galleries](../README.md#sample-galleries) after the first web part, and inspect each sample's package versions before running it.

## Environment and Debugging

- Record the project's Node.js version in a version-manager configuration and document the matching SPFx release. Use the [compatibility matrix](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/compatibility) when switching between projects; the newest Node.js or React release is not automatically supported.
- Keep the generated lockfile under source control. Use `npm ci` for reproducible installations in CI; update dependencies intentionally when the lockfile needs to change. See [npm ci](https://docs.npmjs.com/cli/v11/commands/npm-ci).
- Set `SPFX_SERVE_TENANT_DOMAIN` and review `config/serve.json` before starting a sample. For modern SPFx, use a development tenant: the [local workbench was removed in SPFx 1.13](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/release-1.13.0).
- Use browser Network and Console panels together. A certificate rejection, missing manifest, API permission error, and JavaScript exception need different fixes; start with the failing request or first exception.
- Test extensions on actual SharePoint pages with the [Debug Toolbar](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/debug-toolbar). Exercise navigation, edit mode, and multiple component instances as well as a fresh page load.
- Review a [CLI for Microsoft 365 upgrade report](https://pnp.github.io/cli-microsoft365/cmd/spfx/project/project-upgrade/) on a branch before applying its generated script. Rebuild and test a deployed package after changing the toolchain.

## Data Access

- Configure a PnPjs client with the current SPFx context in a service, then pass that service to the UI. Keep mock and live implementations behind the same interface so loading, empty, and permission-error states are easy to exercise. See [PnPjs in SPFx](https://pnp.github.io/pnpjs/concepts/auth-spfx/).
- Request only the fields the component renders. Filter on the server and page results instead of downloading an entire list for a small view. For large lists, design indexed filters and review [SharePoint list throttling guidance](https://learn.microsoft.com/en-us/sharepoint/dev/general-development/how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online).
- With PnPjs batching, queue the requests before calling `execute()`. Awaiting an individual batched request before executing the batch prevents progress. Create a new batch for the next group of operations, and follow the [batching examples](https://pnp.github.io/pnpjs/concepts/batching/).
- Treat a batch as a transport optimization, not a transaction. A successful outer response does not guarantee every operation succeeded; inspect individual results and retry only failed operations. SharePoint batch changes are [not transactional](https://learn.microsoft.com/en-us/sharepoint/dev/sp-add-ins/make-batch-requests-with-the-rest-apis).
- Give caches explicit expiry and invalidation rules. Include the tenant, site, user, and query inputs in keys when results depend on them; invalidate affected data after writes. Avoid persisting sensitive results unnecessarily. See [PnPjs caching behaviors](https://pnp.github.io/pnpjs/queryable/behaviors/).
- Respect `Retry-After` on throttled Graph calls and use bounded backoff when it is absent. Batch requests can be throttled individually; batching does not bypass service limits. See [Graph throttling guidance](https://learn.microsoft.com/en-us/graph/throttling).
- For a 403, check both the user's access to the resource and any required API approval. Declaring `webApiPermissionRequests` requests consent; it does not grant it. Use [AadHttpClient guidance](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/use-aadhttpclient) for protected custom APIs.

## Rendering and Performance

- Keep expensive requests out of `render()`. Fetch in a service or effect with explicit dependencies, and ignore stale responses when filters change rapidly or the component unmounts.
- Debounce text-based searches and avoid fetching until required configuration exists. Display a useful configuration or empty state while there is nothing to query.
- Load large charting, export, and editor libraries only when their features are used. Move authoring-only imports behind `loadPropertyPaneResources()` when appropriate; the [SPFx dynamic-loading guide](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/dynamic-loading) shows both patterns.
- Measure a production build on a real page with realistic data and several web parts. Compare the bytes loaded and request waterfall before and after an optimization; development builds alone can give misleading results.
- Render a useful loading state, an empty state, a partial-failure state, and a retry action. Keep these states testable with mock data instead of relying on a tenant outage to see them.

## UI and Component Lifecycle

- Use CSS Modules and styles scoped to the component. Avoid targeting SharePoint's internal class names or injecting styles into unrelated page elements; those details can change independently of your code. See [SPFx CSS recommendations](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/css-recommendations).
- Support section backgrounds with `supportsThemeVariants` and the theme service. Test contrast in different section themes, and remove theme-change subscriptions when disposing the component. See [section background support](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/guidance/supporting-section-backgrounds).
- Use semantic buttons and labels, preserve visible focus, and restore focus after closing a dialog. Consult the [ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/) for keyboard interactions in custom widgets.
- For Application Customizers, react to placeholder changes and handle a missing placeholder gracefully. Use the supported [placeholder APIs](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/extensions/get-started/using-page-placeholder-with-extensions) for rendering.
- Clean up timers, observers, listeners, and React mounts when a component is disposed. Test navigation and removal from an edited page to catch duplicate subscriptions.
- Keep user-facing text in localization files, and format dates and numbers for the user's locale. Test long translations and right-to-left layouts when relevant; see [localization guidance](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/guidance/localize-web-parts).
- Store secrets in a backend service, never in web-part properties, environment variables bundled into JavaScript, or a client-side configuration file. SPFx runs in the user's browser; review the [enterprise guidance](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/enterprise-guidance) for its trust model.

## Release Checklist

- [ ] Confirm supported Node.js, TypeScript, React, and SPFx dependency versions.
- [ ] Run the project's linting and configured tests, then build and package in production mode.
- [ ] Verify the package version, asset-hosting settings, and intended app-catalog scope.
- [ ] Review API permissions and arrange the required administrator consent separately from package deployment.
- [ ] Test installation and upgrade on a development site with realistic data and a normal user's permissions.
- [ ] Check keyboard operation, focus, contrast, narrow layouts, theme changes, and every supported host.
- [ ] Test empty data, denied access, failed requests, throttling, and multiple instances on a page.
- [ ] Keep the prior package and deployment notes, and confirm a recovery procedure that accounts for any data or provisioning changes.

Use [tenant-scoped deployment guidance](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/tenant-scoped-deployment) before setting `skipFeatureDeployment`: tenant-wide availability changes how components are installed and limits feature-based provisioning. Review [SharePoint CSP guidance](https://learn.microsoft.com/en-us/sharepoint/dev/spfx/content-securty-policy-trusted-script-sources) for externally loaded scripts.

## Practice Projects

These are suggested exercises, not claims that a linked sample implements every requirement.

| Project | Skills to practice | Definition of done |
| --- | --- | --- |
| List explorer | Typed services, list picker, filtering, and pagination. | Select a list and browse bounded pages with loading, empty, and denied-access states. |
| Analytics dashboard | Aggregation, chart loading, accessible alternatives, and theme support. | Render a filtered chart and equivalent data table; verify two instances can use different lists. |
| Personal task panel | Microsoft Graph, consent, and delegated user context. | Explain required permissions and handle sign-in, denied access, and empty results. |
| Application Customizer banner | Supported placeholders, navigation, and cleanup. | Navigate between pages without duplicate banners or handlers. |
| Viva Connections card | Card views, quick views, and focused dashboard interactions. | Display a useful summary and complete one action from a quick view. |
| Release pipeline | Reproducible install, tests, packaging, and controlled deployment. | Produce a versioned package and verify its upgrade on a development site. |

For dashboard and workflow inspiration, explore [Ahmed Makroum's SPFx Library](https://github.com/ahmedmakroum/spfx-library). Its mock-data demos provide examples to inspect and adapt; production data integrations depend on the individual web part.
