---
name: update-github-info
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
engine:
  id: copilot
  copilot-sdk: true
tools:
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
    branch-prefix: github-info/
    draft: false
---

Read `notes/mona-notes.md` first. Use the web-fetch tool to read:

- https://github.blog/latest/
- https://github.blog/changelog/

Update `site/content/github-info.md` with concise, practical information that
helps developers learn GitHub faster. Use only useful, relevant updates from
these official sources, avoid duplicating existing content, and identify the
source for each update.

When the page changes, create a pull request targeting `main` for Mona to
review. Summarize the changes and their sources in the pull request, and
explicitly ask Mona to review them. Do not write directly to `main`; use the
configured create-pull-request safe output.

If there is nothing useful to add, leave the page unchanged and call `noop`
with a brief explanation.
