# Kotlin Style Guide Skill for AI Coding Agents

<div align="center">
  <p>The official Android Kotlin style guide, packaged as an AI coding agent skill.</p>
</div>

---

Give your AI coding agent — Cursor, Claude, GitHub Copilot, Windsurf, or any AI tool — instant access to the official Kotlin style guide from the Android documentation. These aren't just docs; they're production-ready coding standards for Kotlin code on Android.

> **1 language style guide** — Kotlin, formatted for AI agent consumption.

---

## Table of Contents

- [Who Is This For](#who-is-this-for)
- [Why This Style Guide](#why-this-style-guide)
- [Quick Start](#quick-start)
- [Available Style Guides](#available-style-guides)
- [How It Works](#how-it-works)
- [License](#license)

---

## Who Is This For

- **Developers using AI coding agents** who want consistent, standard-conforming Kotlin code generation
- **Teams adopting the Kotlin style guide** across their Android codebase
- **Anyone tired of inconsistent AI-generated code** that doesn't follow best practices
- **Engineering managers** enforcing coding standards

---

## Why This Style Guide?

AI agents generate code that works but often violates style conventions. Wrong naming, inconsistent formatting, anti-patterns — the same issues, over and over.

This guide packages the official Android Kotlin style guide in a format AI agents can reference during code generation. The result: code that follows industry-standard conventions from the first keystroke.

Source: https://developer.android.com/kotlin/style-guide

---

## Quick Start

The `skills` CLI copies style guide content into your project so AI coding agents can reference these standards when generating code.

### Install All Style Guides

```bash
npx skills add achanu/kotlin-styleguide-skills
```

### Install Individual Style Guides

# Mobile
```bash
npx skills add achanu/kotlin-styleguide-skills/kotlin
```

---

## Available Style Guides

| Language | Command | What's Covered |
| --- | --- | --- |
| **Kotlin** | `npx skills add achanu/kotlin-styleguide-skills/kotlin` | Naming, formatting, braces, whitespace, KDoc |

---

## How It Works

1. **Install the skill** using `npx skills add`
2. **The style guide is copied** to your agent's skills directory
3. **Your AI agent reads it** when generating Kotlin code
4. **Generated code follows** the official style conventions automatically

The skills system integrates with:
- Cursor
- Claude
- GitHub Copilot
- Windsurf
- Any AI coding tool that supports context injection

---

## License

This project is licensed under the [MIT License](LICENSE).

Copyright (c) 2026 achanu

---

<div align="center">
  Content derived from the <a href="https://developer.android.com/kotlin/style-guide">official Android Kotlin style guide</a>
</div>
