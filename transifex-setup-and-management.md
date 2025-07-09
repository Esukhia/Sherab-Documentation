# Transifex Setup and Management for Open edX

The Open edX platform stores all its translation files in the [openedx-translations](https://github.com/openedx/openedx-translations) repository.

To simplify the process of managing or customizing localization, this guide outlines how to set up and manage a Transifex project for the `openedx-translations` repository.

---

## 🚀 Project Setup Approaches

There are multiple ways to connect and manage translation files with Transifex. Depending on your workflow and preferences, choose one of the following methods:

---

### 📁 Manual Approach

**Manual File Uploads**

- Upload translation source files (e.g., `.po`, `.json`) directly from your local system.

- Transifex Guide: [Uploading content for translation](https://help.transifex.com/en/articles/6236812-uploading-content-for-translation)

**Manual Translation Uploads**

- You can upload translated files manually for specific languages.
- Transifex Guide: [Uploading translations](https://help.transifex.com/en/articles/6318456-uploading-translations)

---

### 🐍 API (Python SDK) Approach

Use Transifex's Python SDK to programmatically push and pull translation resources.

- Transifex API Reference: [Python SDK Docs](https://developers.transifex.com/reference/api-python-sdk)

---

### 🔧 CLI (Command Line Interface)

The Transifex CLI (`tx`) is ideal for automated and scriptable workflows.

- Setup Guide: [Transifex CLI Documentation](https://developers.transifex.com/docs/cli)

Useful commands:

    tx init # Initialize a new .tx config
    tx push -s # Push source files
    tx push -t # Push translations
    tx pull -a # Pull all available translations

---

### 🔗 GitHub Integration (Recommended)

We are currently using GitHub integration with Transifex. This provides a seamless synchronization between your repository and Transifex projects.

- Transifex Docs: [GitHub installation and configuration](https://help.transifex.com/en/articles/6265125-github-installation-and-configuration)
- GitHub App: [Transifex Integration](https://github.com/apps/transifex-integration)

**Benefits:**

- Automatic syncing of translation files on PRs and commits
- Easy configuration via `transifex.yml` file
- Continuous localization workflows

---

### 📚 Guide for Setup and Management

- 🔗 [Transifex Integration with GitHub](./docs-resources/transifex/transifex-github-integration.md)
- 🔐 [Generating a Transifex API Token](./docs-resources/transifex/transifex-token-generation.md)
- 👥 [User Roles and Access in Transifex](./docs-resources/transifex/user-roles-access-for-transifex.md)
- 🛠️ [Fixing Transifex Resource Names for Open edX](./docs-resources/transifex/fix-transifex-resource-names-for-openedx.md)
---