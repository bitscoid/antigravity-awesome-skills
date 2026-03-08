# antigravity-awesome-skills Development Patterns

> Auto-generated skill from repository analysis

## Overview

The antigravity-awesome-skills repository is a comprehensive skill registry that manages a collection of AI/coding skills with automated catalog generation and validation. It follows a structured approach where skills are defined in SKILL.md files, automatically indexed into JSON catalogs, and synchronized across multiple documentation formats. The codebase emphasizes automation, consistency, and maintainability through well-defined workflows.

## Coding Conventions

### File Naming
- **Skills**: Use PascalCase for skill directory names (e.g., `skills/DataAnalysis/`, `skills/WebDevelopment/`)
- **Skill files**: Always named `SKILL.md` within skill directories
- **Generated files**: Use lowercase with underscores (e.g., `skills_index.json`)

### Import/Export Style
```python
# Use relative imports for local modules
from .validators import validate_skill
from ..data import catalog_generator

# Mixed export patterns for different file types
# JSON files use structured data export
# Markdown files use template-based generation
```

### YAML Frontmatter Structure
```yaml
---
name: "Skill Name"
description: "Brief description under 200 characters"
category: "primary-category"
tags: ["tag1", "tag2", "tag3"]
difficulty: "beginner|intermediate|advanced"
version: "1.0.0"
---
```

## Workflows

### Skill Addition Workflow
**Trigger:** When someone adds new skill files to the repository
**Command:** `/add-skill`

1. Create new directory under `skills/` using PascalCase naming
2. Add `SKILL.md` file with proper YAML frontmatter and content
3. Run validation checks to ensure proper format and structure
4. Generate updated `skills_index.json` with new skill metadata
5. Update `data/catalog.json` and `data/bundles.json` with categorized entries
6. Regenerate `README.md` with updated skill counts and statistics
7. Update `CATALOG.md` with new skill listings and categories
8. Commit changes with format: `feat: add [SkillName] skill`

### Registry Sync Workflow
**Trigger:** After skill additions, modifications, or catalog updates
**Command:** `/sync-registry`

1. Scan all `skills/*/SKILL.md` files for metadata extraction
2. Generate comprehensive `skills_index.json` with all skill data
3. Rebuild `data/catalog.json` with categorized skill organization
4. Update `data/bundles.json` with skill groupings and collections
5. Regenerate `README.md` with current skill counts and featured skills
6. Update `CATALOG.md` with alphabetically sorted skill listings
7. Validate all generated files for consistency and completeness
8. Commit with format: `chore: sync registry files`

### Release Workflow
**Trigger:** When preparing a new version release with accumulated changes
**Command:** `/release`

1. Update `package.json` with new semantic version number
2. Regenerate `package-lock.json` with updated dependencies
3. Generate or update `CHANGELOG.md` with version history and changes
4. Update `README.md` with version badges and release information
5. Create `release_notes.md` with highlights and breaking changes
6. Run complete catalog regeneration to ensure consistency
7. Tag release with version number
8. Commit with format: `chore: release v[X.Y.Z]`

### Validation Fix Workflow
**Trigger:** When validation errors are detected across multiple skills
**Command:** `/fix-validation`

1. Run comprehensive validation checks on all `skills/*/SKILL.md` files
2. Identify and fix YAML frontmatter syntax errors and missing fields
3. Truncate or revise descriptions exceeding 200 character limit
4. Resolve dangling internal links and broken references
5. Standardize tag formats and category classifications
6. Update affected `SKILL.md` files with corrections
7. Re-run validation to confirm all issues resolved
8. Commit with format: `fix: resolve validation errors in [N] skills`

### Documentation Reorganization Workflow
**Trigger:** When restructuring documentation or cleaning up repository structure
**Command:** `/reorganize-docs`

1. Analyze current documentation structure in `docs/` directory
2. Move, rename, or consolidate documentation files as needed
3. Update `.gitignore` patterns to exclude temporary or generated files
4. Update `README.md` with corrected file references and links
5. Remove duplicate, outdated, or stale documentation files
6. Update `docs/README.md` with new documentation index
7. Validate all internal links and cross-references
8. Commit with format: `docs: reorganize documentation structure`

## Testing Patterns

```javascript
// Testing uses vitest framework with .test.tsx pattern
// Example test structure for validation:
import { describe, it, expect } from 'vitest'
import { validateSkill } from '../validators'

describe('Skill Validation', () => {
  it('should validate proper YAML frontmatter', () => {
    const skillContent = `---
name: "Test Skill"
description: "Valid description"
category: "testing"
---`
    expect(validateSkill(skillContent)).toBe(true)
  })
})
```

## File Structure Patterns

```
skills/
├── SkillName/
│   └── SKILL.md           # Main skill definition
data/
├── catalog.json           # Categorized skill catalog
├── bundles.json          # Skill collections and bundles
└── skills_index.json     # Complete skill index
docs/
├── README.md             # Documentation index
└── *.md                  # Additional documentation
```

## Commands

| Command | Purpose |
|---------|---------|
| `/add-skill` | Add new skills and update all generated registry files |
| `/sync-registry` | Synchronize all generated files after skill changes |
| `/release` | Create versioned releases with changelog and updates |
| `/fix-validation` | Fix validation errors across multiple skill files |
| `/reorganize-docs` | Restructure and clean up documentation files |