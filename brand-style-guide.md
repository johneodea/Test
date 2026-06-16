# Brand Style Guide: Setting Up a Workspace Skill for Cortex Code

## Overview

This guide teaches you how to create a **workspace-level skill** that instructs Cortex Code to apply your corporate brand color palette whenever it generates HTML reports, styled notebooks, or visual outputs.

---

## What Is a Workspace Skill?

A workspace skill is a Markdown file placed in the `.cortex/skills/` directory at the root of your workspace. Cortex Code automatically loads these files into context for every conversation, ensuring consistent behavior across all users and sessions in the workspace.

---

## Step-by-Step Setup

### 1. Create the Directory Structure

In your workspace root, create the following path:

```
.cortex/
  skills/
```

You can do this from the terminal:

```bash
mkdir -p .cortex/skills
```

### 2. Create the Skill File

Create a Markdown file inside `.cortex/skills/`. The filename should be descriptive:

```
.cortex/skills/brand-colors.md
```

### 3. Define Your Brand Palette

Below is a template you can copy and customize with your organization's actual colors.

---

## Template: `.cortex/skills/brand-colors.md`

````markdown
# Corporate Brand Color Palette

When generating HTML reports, dashboards, charts, styled notebook outputs,
or any visual content, always apply the following brand guidelines.

## Primary Colors

| Role            | Color Name     | Hex Code  | Usage                                    |
|-----------------|----------------|-----------|------------------------------------------|
| Primary         | Brand Blue     | #1B3A6B   | Headers, primary buttons, key highlights |
| Secondary       | Brand Teal     | #2AAFCB   | Links, accents, chart emphasis           |
| Background      | Light Gray     | #F4F6F8   | Page backgrounds, alternating table rows |
| Surface         | White          | #FFFFFF   | Card backgrounds, content areas          |
| Text Primary    | Dark Charcoal  | #2D2D2D   | Body text, labels                        |
| Text Secondary  | Medium Gray    | #6B7280   | Captions, secondary information          |

## Accent / Chart Colors

Use these colors in sequence for multi-series charts and visualizations:

1. `#2AAFCB` (Teal)
2. `#1B3A6B` (Blue)
3. `#F4A261` (Amber)
4. `#E76F51` (Coral)
5. `#2A9D8F` (Green)
6. `#9B5DE5` (Purple)

## Typography

- **Headings:** font-family: 'Segoe UI', Arial, sans-serif; font-weight: 600
- **Body text:** font-family: 'Segoe UI', Arial, sans-serif; font-weight: 400
- **Code/Data:** font-family: 'Cascadia Code', 'Courier New', monospace

## HTML Report Structure

When generating an HTML report, always include:

1. A **branded header bar** with the Primary color as background and white text
2. A **consistent container** with max-width: 960px and centered alignment
3. **Tables** styled with:
   - Header row: Primary color background, white text
   - Alternating rows: Light Gray / White
   - Border: 1px solid #E5E7EB
4. **Status indicators:**
   - Success/Good: #10B981
   - Warning/Caution: #F59E0B
   - Error/Critical: #EF4444
   - Informational: #3B82F6

## Example CSS Block

Include this CSS in all generated HTML reports:

```css
:root {
  --brand-primary: #1B3A6B;
  --brand-secondary: #2AAFCB;
  --brand-bg: #F4F6F8;
  --brand-surface: #FFFFFF;
  --brand-text: #2D2D2D;
  --brand-text-secondary: #6B7280;
  --brand-border: #E5E7EB;
  --brand-success: #10B981;
  --brand-warning: #F59E0B;
  --brand-error: #EF4444;
  --brand-info: #3B82F6;
}

body {
  font-family: 'Segoe UI', Arial, sans-serif;
  background-color: var(--brand-bg);
  color: var(--brand-text);
  margin: 0;
  padding: 0;
}

.report-header {
  background-color: var(--brand-primary);
  color: #FFFFFF;
  padding: 1.5rem 2rem;
  font-size: 1.25rem;
  font-weight: 600;
}

.report-container {
  max-width: 960px;
  margin: 2rem auto;
  padding: 2rem;
  background: var(--brand-surface);
  border-radius: 8px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

table {
  width: 100%;
  border-collapse: collapse;
  margin: 1.5rem 0;
}

th {
  background-color: var(--brand-primary);
  color: #FFFFFF;
  padding: 0.75rem 1rem;
  text-align: left;
  font-weight: 600;
}

td {
  padding: 0.75rem 1rem;
  border-bottom: 1px solid var(--brand-border);
}

tr:nth-child(even) {
  background-color: var(--brand-bg);
}
```

## Important Notes

- Never override these colors with default or generic styles
- If a report requires additional colors beyond the palette, derive them
  by adjusting opacity of existing brand colors (e.g., rgba(27, 58, 107, 0.1))
- Always maintain WCAG AA contrast ratios for text readability
- Logo placement: top-left of the header bar when applicable
````

---

## How It Works

Once the file is saved at `.cortex/skills/brand-colors.md`:

1. **Automatic loading** - Cortex Code detects the file on every new conversation in the workspace
2. **Consistent enforcement** - Any request to generate HTML, styled output, or charts will follow the palette
3. **No manual prompting** - Analysts don't need to remind Cortex Code about the brand; it's always in context

---

## Customization Tips

| Want to change...          | Edit this section...                  |
|----------------------------|---------------------------------------|
| Company colors             | Primary Colors table                  |
| Chart color sequence       | Accent / Chart Colors list            |
| Fonts                      | Typography section                    |
| Report layout rules        | HTML Report Structure section         |
| CSS variables              | Example CSS Block                     |

---

## Verifying It Works

After creating the skill file, start a new conversation in the workspace and ask Cortex Code to generate a sample HTML report. It should automatically apply your brand colors without any additional prompting.

**Test prompt:**
> "Generate a sample HTML report showing quarterly revenue by region."

The output should use your defined header color, table styling, and chart palette.

---

## Multiple Skills

You can add additional skill files for other standards:

```
.cortex/skills/brand-colors.md       # Color palette and visual styling
.cortex/skills/sql-standards.md      # SQL naming conventions and formatting
.cortex/skills/report-templates.md   # Standard report structures
```

Each file is loaded independently, so keep them focused on a single concern.
