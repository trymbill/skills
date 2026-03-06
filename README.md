<p align="center">
  <img src="https://img.shields.io/badge/agent_skills-trymbill-8B5CF6?style=for-the-badge&labelColor=1a1a2e" alt="Agent Skills" />
  <img src="https://img.shields.io/badge/skill-find--bugs-10B981?style=for-the-badge&labelColor=1a1a2e" alt="find-bugs" />
</p>

<h1 align="center">🔍 trymbill/skills</h1>

<p align="center">
  <strong>Agent skills to supercharge your coding workflow.</strong><br/>
  Currently featuring <code>find-bugs</code> — a skill that reviews your code changes for bugs, security vulnerabilities, and quality issues.
</p>

<p align="center">
  <a href="https://skills.sh/trymbill/skills/find-bugs">View on skills.sh</a> ·
  <a href="https://github.com/trymbill/skills/issues">Report Issue</a> ·
  <a href="https://github.com/trymbill/skills">Source</a>
</p>

---

## Available Skills

| Skill | Description |
| :--- | :--- |
| **[find-bugs](./find-bugs)** | Detect bugs, security vulnerabilities, and code quality issues in your local branch changes. Great for pre-review sanity checks. |

---

## Quick Install

The fastest way to get started is through [**skills.sh**](https://skills.sh) — the open agent skills ecosystem.

```bash
npx skills add trymbill/skills
```

This auto-detects your installed coding agents (Claude Code, Cursor, Copilot, Codex, Windsurf, etc.) and installs the skills to the right location.

### Install a specific skill

```bash
npx skills add trymbill/skills --skill find-bugs
```

### Install globally (user-level)

```bash
npx skills add trymbill/skills -g
```

> **Tip:** Add `-y` to skip confirmation prompts: `npx skills add trymbill/skills -gy`

---

## Other Installation Methods

<details>
<summary><strong>🔧 Manual install (git clone)</strong></summary>

<br/>

Clone the repo and copy the skill directory into your agent's skill folder:

```bash
git clone https://github.com/trymbill/skills.git
```

Then copy the skill you want into your project or user-level config:

**Claude Code**
```bash
cp -r skills/find-bugs .claude/skills/find-bugs
```

**GitHub Copilot**
```bash
cp -r skills/find-bugs .github/skills/find-bugs
```

**Codex / OpenCode**
```bash
cp -r skills/find-bugs .codex/skills/find-bugs
```

**User-level (available across all projects)**
```bash
cp -r skills/find-bugs ~/.claude/skills/find-bugs
```

</details>

<details>
<summary><strong>🔗 Symlink for multi-project setups</strong></summary>

<br/>

If you work across many repos, symlink from a central location:

```bash
# Clone once
git clone https://github.com/trymbill/skills.git ~/agent-skills/trymbill

# Symlink into any project
ln -s ~/agent-skills/trymbill/find-bugs /path/to/your-project/.claude/skills/find-bugs
```

</details>

<details>
<summary><strong>📦 Claude Code plugin marketplace</strong></summary>

<br/>

If the repo is registered as a plugin marketplace, you can install directly from Claude Code:

```
/plugin marketplace add trymbill/skills
```

</details>

---

## Usage

Once installed, the skill activates automatically when you ask your agent to review code or find bugs. Try prompts like:

- *"Review my changes for bugs"*
- *"Find security issues in this branch"*
- *"Audit the code I changed"*
- *"Are there any bugs in my diff?"*

The agent will analyze your local branch changes, flag issues by severity, and report findings — without making any changes to your code.

---

## Keeping Skills Up to Date

```bash
# Check for updates
npx skills check

# Update all installed skills
npx skills update
```
