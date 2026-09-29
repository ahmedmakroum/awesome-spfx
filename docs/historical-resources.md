# Historical and Migration Resources

[Back to Awesome SPFx](../README.md)

These resources remain useful for understanding older solutions or planning adjacent SharePoint work. Inspect their dependency versions, external services, and deployment scripts before reusing code.

## Older Samples

- [SPFx Fantastic 40 Web Parts](https://github.com/OlivierCC/spfx-40-fantastics) - Early SPFx collection of galleries, carousels, charts, maps, and editors; use for design inspiration and reassess its dependencies and external integrations.
- [SharePoint Starter Kit](https://github.com/pnp/sp-starter-kit) - Intranet showcase with web parts, extensions, and provisioning; its v3 documentation targets SPFx 1.16.1 and the scripts change tenant-level settings.
- [React Jest testing sample](https://github.com/pnp/sp-dev-fx-webparts/tree/main/samples/react-jest-testing) - PnP example of Jest and Enzyme testing for an older SPFx stack; inspect its package versions before adapting the setup.

For new work, start with the [current sample galleries](../README.md#sample-galleries) and [testing resources](../README.md#testing-and-cicd).

## SharePoint Content Migration Tools

These tools move SharePoint content. They do not automatically rewrite custom web parts, convert Add-ins to SPFx, or upgrade an SPFx project's source code.

- [ShareGate](https://sharegate.com/download-migration-tool) - Commercial Microsoft 365 content migration and governance tool.
- [SharePoint Migration Tool](https://learn.microsoft.com/en-us/sharepointmigration/how-to-use-the-sharepoint-migration-tool) - Microsoft tool for migrating content from supported on-premises sources to Microsoft 365.

For code modernization, use the [migration and upgrade resources](../README.md#migration-and-upgrades).
