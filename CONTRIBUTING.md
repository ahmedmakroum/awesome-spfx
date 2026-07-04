# Contributing Guidelines

Thanks for taking the time to contribute! Please follow these guidelines to help your pull request get merged quickly.

## Guidelines

- Search existing entries first to avoid duplicates.
- Make sure the resource is related to SharePoint Framework (SPFx) development.
- Add one link per pull request. This makes review easier and keeps history clean.
- Add links to the bottom of the relevant category, in alphabetical order.
- Use this format:

  ```markdown
  - [Name](link) - Description.
  ```

  The description should start right after the link and explain, in one concise sentence, what the resource is and why it's useful. Start the description with a capital letter and end it with a period.

- Keep pull requests focused: one entry, one commit, no unrelated changes to formatting or other entries.
- Check your spelling and grammar.
- New categories are welcome, but open an issue to discuss before submitting a pull request.

## What makes a good addition

- The project or resource is actively maintained, or is a stable/finished reference that is still accurate today.
- The link works (no 404s, no parked domains, no paywalled-only content).
- It isn't purely self-promotional with no clear value to the community.
- It isn't already covered by an existing, better-maintained entry in the same category.

## Removing entries

If you find a dead link, an archived/abandoned project, or an entry that no longer fits, please open a pull request removing it (or open an issue if you're not sure).

## Quality checks

Every pull request is automatically checked with [awesome-lint](https://github.com/sindresorhus/awesome-lint) via GitHub Actions. Please make sure your change passes lint locally before submitting:

```sh
npx awesome-lint
```

Thank you for contributing! 
