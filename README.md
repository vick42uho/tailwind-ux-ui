# Tailwind CSS Premium UX/UI Design System Skill

A reusable agent skill for Google Antigravity and other AI coding assistants (like Claude Code, Codex, etc.) that equips the agent with a deep, comprehensive guidelines and implementation ruleset for crafting web applications that match the premium visual design, layout architectures, and UX details of the official [tailwindcss.com](https://tailwindcss.com/) site.

Based on the core principles of **Refactoring UI**.

## 🚀 Installation

### For Google Antigravity 2.0

#### Global Installation (Available across all projects)

1. Clone or download this repository.
2. Copy the `tailwind-ux-ui` folder containing `SKILL.md` into your global skills directory:
   * **Windows**: `%USERPROFILE%\.gemini\config\skills\tailwind-ux-ui\`
   * **macOS/Linux**: `~/.gemini/config/skills/tailwind-ux-ui/`
3. Add the skill entry to your `.datacloud_skills_manifest` file located in the parent `skills` directory:
   ```json
   "tailwind-ux-ui": {
     "status": "installed",
     "checksum": "<SHA256-checksum-of-SKILL.md>"
   }
   ```
   *(To calculate the checksum on Windows PowerShell, run: `Get-FileHash -Path .\SKILL.md -Algorithm SHA256`)*

#### Local Installation (Project-specific)

Copy the `tailwind-ux-ui` folder into your project's local agent skills directory:
* **Antigravity / Codex**: `.agents/skills/tailwind-ux-ui/SKILL.md`
* **Claude Code**: `.claude/skills/tailwind-ux-ui/SKILL.md`
* **Gemini CLI**: `.gemini/skills/tailwind-ux-ui/SKILL.md`

---

## 📖 Contents of the Skill

* **Core Principles**: Refactoring UI mindset, designing in grayscale first, hierarchy contrast rules.
* **Spacing Scale**: The 4px grid rules, component padding ratios (2:1 horizontal-to-vertical).
* **Typography Grid**: Dynamic Tracking (letter-spacing) and Leading (line-height) rules for sharp headings.
* **Color System**: Slate & Zinc palette guidelines, Dynamic Semantic contrast scales, hover and active focus rings.
* **Elevation & Borders**: Soft shadow values, rounded card rules, and glassmorphic panels.
* **Dark Mode Architecture**: Contrast adjustments, background levels, white-opacity borders.
* **Visual Accents**: Tailwind's signature SVG mesh grid backdrops and radial color glows.
* **Code Templates**: Interactive cards and standard 3-column documentation layouts.

---

## 📄 License

Apache-2.0 License. Feel free to use and distribute!
