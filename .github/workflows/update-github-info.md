---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
engine: copilot
tools:
  github:
    toolsets: [repos]
  edit:
  web-fetch:
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    base-branch: main
    draft: true
    title-prefix: "[mona] "
---

# Update GitHub Info

Keep Mona's GitHub Info website current with concise, practical updates from official GitHub sources.

## Research

1. Read `notes/mona-notes.md` before drafting anything.
2. Use the `web-fetch` tool to fetch and read https://github.blog/latest/.
3. Use the `web-fetch` tool to fetch and read https://github.blog/changelog/.
4. Use the GitHub repository API tools, not terminal, CLI, or sandboxed commands, to read repository guidance and reference files needed for this task.
5. Use the `edit` tool to update only `site/content/github-info.md`.

## Editorial requirements

- Keep summaries short and practical for developers learning GitHub.
- Attribute every update sourced from the GitHub Blog or GitHub Changelog with a link to its source.
- Preserve the existing editorial angle and homepage themes.
- Make changes only when there is a meaningful, well-supported update; otherwise leave the content unchanged.

## Review workflow

After updating the content, inspect the final diff for accuracy, scope, and accidental changes. Use the `create-pull-request` safe output exactly once to open a draft pull request targeting `main` for Mona to review. Include a concise summary of the sources consulted and the content changes in the pull request body. Do not write directly to `main`, push manually, or modify any other file.
