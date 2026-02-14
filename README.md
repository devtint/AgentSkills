# Agent Skills

A collection of reusable [GitHub Copilot custom skills](https://code.visualstudio.com/docs/copilot/copilot-customization) for VS Code.

## Available Skills

| Skill | Description |
|-------|-------------|
| [clarity-ui](clarity-ui/) | Build clean, minimalist, professional website UIs with light color palettes, glassmorphism, generous whitespace, and polished micro-interactions. |

## Usage

1. Copy the skill folder you want into your workspace or user-level `.copilot/skills/` directory:

   ```
   # Per-workspace
   <project>/.copilot/skills/clarity-ui/SKILL.md

   # Per-user (global)
   ~/.copilot/skills/clarity-ui/SKILL.md
   ```

2. Reference it in your `.github/copilot-instructions.md` or VS Code settings so Copilot Chat picks it up automatically.

3. When you ask Copilot to build a UI, it will follow the design system defined in the skill — warm off-whites, frosted glass cards, amber accents, Outfit typography, and more.

## Contributing

To add a new skill, create a folder with a `SKILL.md` file following the same frontmatter format:

```markdown
---
name: your-skill-name
description: One-line description of what the skill does.
---

Full skill instructions here...
```

## License

MIT
