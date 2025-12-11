# New Project Checklist

Step-by-step guide to set up the AI workflow system in a new project.

---

## Prerequisites

- [ ] Docker installed and running
- [ ] VS Code with Dev Containers extension (`ms-vscode-remote.remote-containers`)
- [ ] Claude Code CLI installed globally (or will install in container)
- [ ] Template folder location known

---

## Step 1: Create Project Structure

```bash
# Create project folder
mkdir my-new-project
cd my-new-project

# Initialize git (optional but recommended)
git init
```

---

## Step 2: Copy Portable Folders

```bash
# From your template location, copy these folders:
cp -r /path/to/template/.ai .
cp -r /path/to/template/.claude .
cp -r /path/to/template/.devcontainer .
cp /path/to/template/CLAUDE.md .
cp /path/to/template/.gitignore .
```

Or if you have the template as a zip:
```bash
unzip ai-workflow-template.zip -d .
```

---

## Step 3: Create Project-Specific Directories

```bash
mkdir -p docs/tasks/completed
mkdir -p docs/working
mkdir -p docs/archive
```

---

## Step 4: Create Project-Specific Files

```bash
# Copy templates and rename
cp .ai/templates/SOLUTION_ARCHITECTURE_TEMPLATE.md SOLUTION_ARCHITECTURE.md
cp .ai/templates/DEV_CONTEXT_TEMPLATE.md dev_context.md
```

Then edit these files:
- [ ] `SOLUTION_ARCHITECTURE.md` - Define your project structure
- [ ] `dev_context.md` - Set your name, initial task

---

## Step 5: Customize Dev Container (if needed)

Edit `.devcontainer/devcontainer.json`:

- [ ] Change `"name"` to your project name
- [ ] Adjust features (Python version, add/remove Node, etc.)
- [ ] Add VS Code extensions you need
- [ ] Modify `postCreateCommand` for your dependencies

See `.devcontainer/CUSTOMIZATION_GUIDE.md` for details.

---

## Step 6: Open in Container

1. Open project in VS Code
2. `Ctrl+Shift+P` → "Dev Containers: Reopen in Container"
3. Wait for container to build (first time takes a few minutes)

---

## Step 7: Authenticate Claude

Inside the container terminal:
```bash
claude auth login
```

Follow the browser prompt to authenticate.

> **Note:** You need to re-authenticate after container rebuild.

---

## Step 8: Verify Setup

```bash
# Check Claude is working
claude --version

# Check slash commands are available
ls .claude/commands/

# Check AI system files
ls .ai/
```

---

## Step 9: Start Working!

In VS Code with Claude Code extension, or in terminal:
```
/start-session
```

Or ask Claude to "run the start-session workflow".

---

## Quick Verification Checklist

After setup, verify:

- [ ] Container running (check Docker or VS Code status bar)
- [ ] `claude --version` works in container terminal
- [ ] `.claude/commands/` folder exists with 6 `.md` files
- [ ] `.ai/` folder exists with workflows, standards, templates, guides
- [ ] `CLAUDE.md` exists in project root
- [ ] `SOLUTION_ARCHITECTURE.md` created and customized
- [ ] `dev_context.md` created and customized
- [ ] `docs/tasks/`, `docs/working/`, `docs/archive/` directories exist

---

## Troubleshooting

### Container won't start
- Check Docker is running
- Check `.devcontainer/devcontainer.json` syntax
- Try "Rebuild Container" from command palette

### Claude auth fails
- Check internet connection from container
- Try `claude auth logout` then `claude auth login` again
- Check API key is valid at console.anthropic.com

### Slash commands not working
- This is a known VS Code extension limitation
- Workaround: Ask Claude to "read and execute .claude/commands/start-session.md"

### Permission errors
- Check file permissions in mounted folders
- On Windows/WSL, may need to adjust Docker settings

---

## Optional: Git Setup

Add to your first commit:
```bash
git add .
git commit -m "chore: Initialize project with AI workflow system"
```

The included `.gitignore` already handles common exclusions.
