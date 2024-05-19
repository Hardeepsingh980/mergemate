# MergeMate: Automated PR Review and Command Handling

MergeMate is an advanced GitHub action designed to automate pull request reviews and handle command-based interactions within GitHub issues. It integrates state-of-the-art AI from OpenAI to provide insightful, context-aware responses to code reviews and comments directly within your GitHub workflow.

## Features

- **Automated PR Reviews**: Automatically generate detailed reviews for pull requests, including code suggestions and best practices.
- **Command Handling**: Respond to commands in PR comments such as `/help`, `/explain`, `/status`, and `/ask` to facilitate more dynamic and interactive PR discussions.
- **Markdown Support**: Enhances readability and user interaction by formatting responses in Markdown with customized headers and footers.
- **Easy Integration**: Designed to work seamlessly as a GitHub action, allowing for straightforward integration into any project's CI/CD pipeline.

## Installation

MergeMate can be easily installed via pip:

```bash
pip install mergemate
```

This single command prepares your environment to leverage MergeMate's capabilities, streamlining your project's interaction paradigms.

## GitHub Action Setup

MergeMate can be integrated into your GitHub workflows with the following configuration:

### Workflow Definition

```yaml
name: Automated PR Review and Command Handling

on:
  pull_request:
    types: [opened, synchronize]
  issue_comment:
    types: [created]

permissions:
  issues: write
  pull-requests: write

jobs:
  review_pull_request:
    if: ${{ github.event_name == 'pull_request' }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.9'
      - name: Install dependencies
        run: pip install mergemate
      - name: Review PR
        run: python -m mergemate.scripts.github.pr_review
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}

  handle_comment:
    if: ${{ github.event_name == 'issue_comment' && github.event.issue.pull_request && startsWith(github.event.comment.body, '/') }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.9'
      - name: Install dependencies
        run: pip install mergemate
      - name: Handle Comment
        run: python -m mergemate.scripts.github.comment_handler
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
```

This workflow automates PR reviews and handles specific commands in comments on pull requests. The configuration is optimized for GitHub actions, ensuring that the operations are only triggered under appropriate conditions to maintain efficiency and resource utilization.

## Documentation

Comprehensive documentation is available within the package, detailing setup instructions, configuration options, and command details. This ensures that all potential users, from novices to seasoned developers, can effectively utilize and customize MergeMate according to their specific needs.

## Contribution

Contributions to MergeMate are welcomed. If you're interested in enhancing its capabilities or tailoring it to fit new use cases, please fork the repository and submit your pull requests. MergeMate is a living project, and contributions help it stay at the cutting edge of technology and usability.

## Licensing

MergeMate is released under the MIT license, which provides great flexibility for both personal and commercial use, encouraging a broad adoption and diverse contributions from the community.

---

MergeMate represents a leap forward in automating interactions within GitHub's ecosystem, reflecting the ongoing evolution in development practices facilitated by advances in AI technology. As we continue to enhance its capabilities, your feedback and contributions are invaluable in shaping its future trajectory.