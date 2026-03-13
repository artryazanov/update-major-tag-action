# Update Major Tag Action

[![Latest Release](https://img.shields.io/github/v/release/artryazanov/update-major-tag-action?sort=semver)](https://github.com/artryazanov/update-major-tag-action/releases)
[![Lint Workflows and Action](https://github.com/artryazanov/update-major-tag-action/actions/workflows/lint.yml/badge.svg)](https://github.com/artryazanov/update-major-tag-action/actions/workflows/lint.yml)
[![Release Tag Updater](https://github.com/artryazanov/update-major-tag-action/actions/workflows/release.yml/badge.svg)](https://github.com/artryazanov/update-major-tag-action/actions/workflows/release.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

A lightweight GitHub Action that automatically updates the major version tag (e.g., `v1`) to always point to the latest release (e.g., `v1.2.3`). This allows users of your actions or packages to subscribe to major updates seamlessly.

## 🚀 Usage

Create a workflow in your repository (e.g., `.github/workflows/release.yml`) that triggers when a release is published:

```yaml
name: Update Major Tag

on:
  release:
    types: [published]

jobs:
  update-tag:
    runs-on: ubuntu-latest
    permissions:
      contents: write # ⚠️ Required to push the tag

    steps:
      - name: Checkout repository
        uses: actions/checkout@v6
        with:
          fetch-depth: 0 # ⚠️ Required: Must fetch all history to work with tags properly

      - name: Update Major Tag
        uses: artryazanov/update-major-tag-action@v1
        # Optionally, you can explicitly pass the tag:
        # with:
        #   tag: ${{ github.event.release.tag_name }}
```

## ⚠️ Important Requirements

1. **`actions/checkout@v6` with `fetch-depth: 0`**: The action needs the full Git history and tags downloaded to forcefully move the tag to the correct commit.
2. **Permissions**: The job requires `permissions: { contents: write }` so the GitHub Actions bot can push the new tag to your repository.

## 📝 License

This project is licensed under the MIT License.
