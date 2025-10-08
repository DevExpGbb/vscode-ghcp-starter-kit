---
on:
  schedule:
  - cron: 0 9 * * 1
  stop-after: +30d
  workflow_dispatch: null
permissions: read-all
network: defaults
safe-outputs:
  create-issue:
    title-prefix: ${{ github.workflow }}
source: githubnext/agentics/workflows/weekly-research.md@ddd497457c64b021c3f5b1bed38325ce9e8862b0
timeout_minutes: 15
tools:
  web-fetch: null
  web-search: null
---
# Weekly Research

## Job Description

Do a deep research investigation in ${{ github.repository }} repository, and the related industry in general.

- Read selections of the latest code, issues and PRs for this repo.
- Read latest trends and news from the software industry news source on the Web.

Create a new GitHub issue with title starting with "${{ github.workflow }}" containing a markdown report with

- Interesting news about the area related to this software project.
- Related products and competitive analysis
- Related research papers
- New ideas
- Market opportunities
- Business analysis
- Enjoyable anecdotes

Only a new issue should be created, no existing issues should be adjusted.

At the end of the report list write a collapsed section with the following:
- All search queries (web, issues, pulls, content) you used
- All bash commands you executed
- All MCP tools you used


<!-- You can customize prompting and tools in .github/workflows/agentics/weekly-research.config -->
@include? githubnext/agentics/agentics/weekly-research.config@ddd497457c64b021c3f5b1bed38325ce9e8862b0
