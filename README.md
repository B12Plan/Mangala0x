# Mangala0x
Mangala0x


on:
  workflow_dispatch:
  schedule:
    - cron: 0 0 * * *
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout 🛎️
        uses: actions/checkout@v2

      - name: Generate Sponsors 💖
        uses: JamesIves/github-sponsors-readme-action@v1.2.2
        with:
          token: ${{ secrets.SPONSOR_WORKFLOW_PAT }}
          file: 'README.md'
          minimum: 1399

      - name: Create Pull Request
        uses: peter-evans/create-pull-request@v5.0.1
        with:
          token: ${{ secrets.SPONSOR_WORKFLOW_PAT }}
          branch: "workflow/sponsors"
          title: "🤖 Update Sponsors"
          commit-message: "🤖 Update Sponsors"
          body: "🤖 Automated pull request created by [sponsors action](https://github.com/reworkd/AgentGPT/actions/workflows/sponsors.yml)"
          labels: "documentation"
