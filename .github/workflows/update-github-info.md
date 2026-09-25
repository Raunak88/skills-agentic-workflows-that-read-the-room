---
name: update-github-info
description: Keep the GitHub Info website current with practical, source-attributed updates from the GitHub Blog, Changelog, and Awesome Copilot workflows.
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions: read-all
tools:
  github:
  web-fetch:
  bash: [curl]
  edit:
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    max: 1
    draft: true
---

# Update GitHub Info

Update the GitHub Info website for Mona's review.

## Required reading

1. Read `notes/mona-notes.md`.
2. Use web-fetch to read `https://github.blog/latest/`.
3. Use web-fetch to read `https://github.blog/changelog/`.
4. Use web-fetch to read `https://awesome-copilot.github.com/workflows/`.
  If web-fetch is unavailable, use bash and run `curl -fsSL --max-time 30` for
  each of these three public URLs. Do not report a missing source until those
  fallback commands have been attempted.
5. Use the GitHub repository API tools for all repository guidance and reference-file reads. Do not use terminal, CLI, or sandboxed commands for GitHub API reads.
6. Read the current `site/content/github-info.md` before editing it.

## Update rules

- Keep summaries short and practical for developers learning GitHub faster.
- Select only useful, recent items that fit the site's existing editorial angle.
- Attribute every Blog or Changelog item to its source with a link.
- Preserve the existing Markdown structure and edit only `site/content/github-info.md`.
- Do not update generated files or unrelated content.

After making the update, use the `create-pull-request` safe output to open a pull request containing the change for Mona to review. Use a concise title and explain which official sources informed the update. If there is no meaningful update to publish after successfully reading the sources, do not modify the file and call the appropriate safe output completion tool.
