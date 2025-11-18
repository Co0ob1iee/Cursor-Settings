# 🚀 Cursor AI Project Management Template

Enterprise-grade project management system for Cursor AI with automated documentation, dependency tracking, and workflow automation.

## 📋 Description

A comprehensive template designed to transform Cursor AI into a powerful project management assistant. It delivers automated documentation updates, dependency mapping, code registry tracking, and checkpoint management — all tightly integrated with your development workflow.

## ✨ Features

* **🤖 Automated Documentation**: Auto-updates documentation based on git changes
* **🗺️ Dependency Mapping**: Visual structure mapping and dependency tracking
* **📚 Code Registry**: Centralized registry for functions, classes, and utilities
* **📍 Checkpoint System**: Versioning and rollback capabilities
* **🔒 Security Rules**: Built-in Snyk-based security rule set
* **⚡ Custom Commands**: Preconfigured Cursor commands for common tasks
* **📝 Enterprise Workflow**: PSD-first approach with governance-ready rules

## 🎯 What's Included

```
.cursor/
├── MASTER.md              # Main project state document
├── PROJECT_MAP.md         # Dependency and architecture map
├── CODE_REGISTRY.md       # Function and class registry
├── CHECKPOINTS.md         # Version checkpoint log
├── commands.json          # Cursor automation commands
├── commands/              # Custom command templates
│   ├── review.md
│   ├── security-review.md
│   ├── refactor.md
│   └── ...
├── rules/                 # Cursor AI rules
│   ├── cursorrules.mdc
│   └── snyk_rules.mdc
└── prompt-library/        # Reusable prompts
```

## 🚀 Quick Start

### 1. Copy the Template

```bash
git clone <this-repo> .cursor-template
cp -r .cursor-template/.cursor ./
```

### 2. Initialize Git

```bash
git init
git add .
git commit -m "Initial commit: setup Cursor AI project management"
```

### 3. Customize the Templates

* Update `.cursor/MASTER.md` with your architecture
* Fill in `.cursor/PROJECT_MAP.md` with your dependencies
* Adjust `.cursor/rules/cursorrules.mdc` to match your standards

### 4. Start Using Cursor Commands

* Press **Cmd/Ctrl + Shift + P** in Cursor
* Select **"Update Project Docs"** after making changes
* Use **"Document This File"** to register new code
* Run **"Create Checkpoint"** to mark stable versions

## 📖 Usage

### Automated Documentation Updates

After each commit, run **"Update Project Docs"** to refresh:

* Completed features in `MASTER.md`
* New dependencies in `PROJECT_MAP.md`
* Newly added functions in `CODE_REGISTRY.md`

### Documenting Code

Use **"Document This File"** to automatically extract metadata from:

* Functions & methods
* Classes & interfaces
* React hooks & components
* API endpoints

### Creating Checkpoints

```bash
git commit -m "feat: add user authentication"
```

Then run **"Create Checkpoint"** to log a stable project state.

## 🔧 Configuration

### Stack Customization

This template is technology-agnostic. Modify:

* `MASTER.md` → Replace `[Technology Stack]`
* `PROJECT_MAP.md` → Adjust diagrams
* `CODE_REGISTRY.md` → Adapt sections to your language or framework

### Cursor Rules

Customize `.cursor/rules/cursorrules.mdc` to define:

* Code quality rules
* Testing requirements
* Documentation conventions
* Security policies

## 📚 Documentation Structure

* **MASTER.md** — Single source of truth
* **PROJECT_MAP.md** — Architecture and dependency map
* **CODE_REGISTRY.md** — Reference for all code elements
* **CHECKPOINTS.md** — Version history

## 🤝 Contributing

Contributions are welcome! You can:

* Add new command templates
* Improve documentation structure
* Expand rulesets
* Suggest features or fixes

## 📄 License

MIT License — use it freely.

## 🙏 Acknowledgments

Built for use with **Cursor AI**, the AI-powered code editor.

---

## ❤️ Support My Work

<p align="center"> <a href="https://patreon.com/Co0ob1iee" target="_blank"> <img src="https://img.shields.io/badge/Support%20on%20Patreon-F96854?style=for-the-badge&logo=patreon&logoColor=white" alt="Patreon"/> </a> &nbsp;&nbsp; <a href="https://buymeacoffee.com/Co0ob1iee" target="_blank"> <img src="https://img.shields.io/badge/Buy%20Me%20a%20Coffee-FFDD00?style=for-the-badge&logo=buymeacoffee&logoColor=black" alt="Buy Me a Coffee"/> </a> </p>
