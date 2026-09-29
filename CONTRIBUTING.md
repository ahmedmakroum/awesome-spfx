# Contributing Guidelines

Thanks for helping maintain Awesome SPFx. Recommend resources you have reviewed and can explain, following the [Awesome manifesto](https://github.com/sindresorhus/awesome/blob/main/awesome.md).

## Adding a Resource

- Search the README and supporting guides to avoid duplicate links.
- Keep additions relevant to SharePoint Framework development.
- Prefer official documentation, maintained projects, and learning material with usable examples.
- Place the entry in the most specific category. Keep the existing learning or topic order; alphabetical ordering is not required.
- Use a direct HTTPS link to the resource, without referral codes or tracking parameters.
- Use this format:

  ```markdown
  - [Name](https://example.com/resource) - Concise description of what it provides and why it is useful.
  ```

- Start the description with a capital letter and end it with a period. Use one entry per line without hard wrapping.
- Label paid courses, previews, and version-specific material clearly. Prefer free learning resources; paid courses should provide a public syllabus or meaningful preview.
- Check SPFx, Node.js, React, and toolchain requirements. Do not imply that the latest version of a general-purpose library is compatible with every SPFx release.
- Describe mock-data demos as demos, and distinguish them from completed production integrations.
- Explain in the pull request why the resource is useful and disclose an affiliation if you maintain it.

## Structure and Scope

- Keep the README a categorized resource directory with a short introduction and an Awesome badge.
- Keep `Contents` as the first section and update its links when adding or renaming headings.
- Include at most one nested level in the contents list. Keep `Contributing` and `Footnotes` out of it.
- Put extended tutorials, command tables, checklists, and tips in `docs/` and link them from the README.
- Keep older reference samples in [historical resources](docs/historical-resources.md), with their limitations explained.
- Add a category when it improves navigation and has enough distinct resources to justify it.
- Keep pull requests focused. A single new resource is usually easiest to review; related corrections or a coherent category update can be grouped.
- Avoid promotional claims, duplicate entries, star-count badges, and links that do not explain their relevance.

## Updating or Removing Entries

Fix redirects, broken anchors, inaccurate descriptions, and outdated setup advice when you find them. Remove dead resources or replace them with a maintained source covering the same need. If an older example is still useful for migration, move it to the historical guide with context.

## Quality Checks

Pull requests are checked with [awesome-lint](https://github.com/sindresorhus/awesome-lint). Run the same command locally:

```sh
npx --yes awesome-lint README.md
```

On Windows, if PowerShell blocks the npm script wrapper, run `npx.cmd --yes awesome-lint README.md`.

Also check any edited supporting guides, relative links, heading anchors, and new external URLs. Awesome-lint checks list conventions; a passing result does not establish that every external resource is available or accurate.
