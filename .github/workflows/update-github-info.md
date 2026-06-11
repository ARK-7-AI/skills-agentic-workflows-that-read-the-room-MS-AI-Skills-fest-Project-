---
engine: copilot
on:
  schedule:
    - cron: 'daily'
  workflow_dispatch:
network:
  allowed:
    - github
    - github.blog
    - github.com
    - awesome-copilot.github.com
tools:
  web-fetch: null
  edit: null
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
  assign-to-agent:
    model: gpt-5-mini
---

# Update GitHub Info

## Purpose

This workflow automatically updates the GitHub Info website with the latest insights from GitHub's official blog and changelog. The workflow collects new information and proposes changes for Mona's review before publication.

## Workflow

### Read Editorial Guidelines

Start by reading the editorial guidelines in `notes/mona-notes.md` to understand what content is suitable for the website.

### Fetch Latest Updates

Web fetch the following sources to gather the latest GitHub news and announcements:
- https://github.blog/latest/ (for latest blog articles)
- https://github.blog/changelog/ (for GitHub changelog entries)
- https://awesome-copilot.github.com/workflows/ (for curated Awesome Copilot workflows)

Also instruct the agent to explicitly web fetch the Awesome Copilot workflows index at `https://awesome-copilot.github.com/workflows/` so curated external workflow examples can be considered as sources.

### Analyze and Summarize

Based on the guidelines and the fetched content, identify 2-3 of the most practical, developer-focused updates that would be relevant to Mona's website audience.

For each update:
- Keep summaries short and practical
- Ensure it helps developers learn GitHub faster
- Always mention the source (e.g., "from GitHub Blog" or "from GitHub Changelog")

### Update Content File

Edit `site/content/github-info.md` to:
1. Update the "Latest GitHub Updates" section with the new updates you've identified
2. Preserve all existing sections (Purpose, Editorial angle, Current homepage themes)
3. Maintain the markdown structure and formatting

### Propose Changes

Create a pull request with the changes:
- Use **safe-outputs** so the changes are proposed without writing directly to main
- Title: "Update: Latest GitHub news and changes"
- Body: Include a brief summary of what was updated and why it's relevant to the website's audience
- Request review from Mona

## Success Criteria

- The workflow completes without errors
- A pull request is created with updated content from github.blog/latest/ or github.blog/changelog/
- All updates follow the editorial guidelines in mona-notes.md
- The PR is ready for Mona's review before merging
