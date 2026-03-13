# antigravity-awesome-skills Development Patterns

> Auto-generated skill from repository analysis

## Overview

This codebase manages a registry of AI skills with automated synchronization workflows. It maintains skill definitions, catalogs, and metadata across multiple formats (Markdown, JSON) with a focus on Azure SDK integrations and web application deployment.

## Coding Conventions

### File Naming
- Use PascalCase for file names: `SkillManager.py`, `CatalogBuilder.py`
- Skill directories: `skills/{skill-name}/SKILL.md`
- Test files: `*.test.*` pattern

### Import Style
```python
# Use relative imports
from .validators import validate_skill
from ..utils import format_metadata
```

### Export Style
```python
# Use named exports
def sync_registry():
    pass

def validate_skills():
    pass

__all__ = ['sync_registry', 'validate_skills']
```

### Commit Messages
- Follow conventional commits with 50 character limit
- Prefixes: `feat:`, `fix:`, `docs:`, `chore:`
- Example: `feat: add azure-cognitive-services skill`

## Workflows

### Skill Registry Sync
**Trigger:** When skills are added, modified, or removed
**Command:** `/sync-registry`

1. Regenerate `CATALOG.md` from skill definitions
2. Update `data/catalog.json` with structured metadata
3. Update `data/bundles.json` for skill groupings
4. Update `skills_index.json` with complete skill listing
5. Verify all cross-references are valid

```bash
# Example sync command
python scripts/sync_registry.py
git add CATALOG.md data/catalog.json data/bundles.json skills_index.json
git commit -m "chore: sync skill registry after updates"
```

### Skill Addition
**Trigger:** When creating a new skill definition
**Command:** `/add-skill`

1. Create `skills/{skill-name}/SKILL.md` with proper frontmatter:
```yaml
---
name: skill-name
description: Brief skill description
category: azure|web|data|ai
difficulty: beginner|intermediate|advanced
tags: [tag1, tag2]
---
```
2. Update `skills_index.json` with new entry
3. Regenerate catalog files using sync workflow
4. Update `package.json` version if needed

### Release Cycle
**Trigger:** When preparing a new version release
**Command:** `/release`

1. Update `package.json` version using semantic versioning
2. Update `CHANGELOG.md` with new features and fixes
3. Update `README.md` with latest skill count and features
4. Run full registry sync to ensure consistency
5. Update `skills_index.json` with release metadata
6. Create git tag: `git tag v{version}`

### Skill Validation Fix
**Trigger:** When skills have YAML frontmatter or formatting issues
**Command:** `/validate-skills`

1. Run validation script: `python scripts/validate_skills.py`
2. Fix YAML frontmatter syntax errors in `skills/*/SKILL.md`
3. Ensure required fields: `name`, `description`, `category`
4. Update `skills_index.json` with corrected metadata
5. Regenerate catalog to reflect fixes

```python
# Example validation check
def validate_skill_frontmatter(skill_path):
    with open(skill_path) as f:
        content = f.read()
    
    # Check for required YAML frontmatter
    if not content.startswith('---'):
        raise ValidationError(f"Missing frontmatter in {skill_path}")
```

### Azure SDK Skill Updates
**Trigger:** When updating Azure service integrations
**Command:** `/update-azure-skills`

1. Identify all `skills/azure-*/SKILL.md` files
2. Standardize descriptions and metadata format
3. Update skill categories and tags consistently
4. Update `skills_index.json` with batch changes
5. Sync catalogs to reflect updates
6. Test Azure SDK version compatibility

### Web App Sync
**Trigger:** When web app needs updated skill data
**Command:** `/sync-web-app`

1. Copy skill files to `web-app/public/skills/*/SKILL.md`
2. Generate `web-app/public/skills.json` from skills index
3. Sync skill metadata for web display
4. Verify JSON schema compatibility
5. Test web app skill loading

```json
// Example web app skills.json structure
{
  "skills": [
    {
      "id": "skill-name",
      "name": "Skill Name",
      "description": "Skill description",
      "path": "/skills/skill-name/SKILL.md"
    }
  ],
  "lastUpdated": "2024-01-15T10:30:00Z"
}
```

## Testing Patterns

Tests follow the `*.test.*` naming pattern and should cover:
- Skill metadata validation
- Registry synchronization accuracy
- JSON schema compliance
- Web app integration

```python
# Example test structure
def test_skill_validation():
    skill_path = "skills/example/SKILL.md"
    assert validate_skill(skill_path) == True

def test_registry_sync():
    sync_registry()
    assert os.path.exists("skills_index.json")
    with open("skills_index.json") as f:
        data = json.load(f)
        assert len(data["skills"]) > 0
```

## Commands

| Command | Purpose |
|---------|---------|
| `/sync-registry` | Regenerate all catalog and index files after skill changes |
| `/add-skill` | Create new skill with proper metadata and update indexes |
| `/release` | Prepare version release with updated documentation |
| `/validate-skills` | Fix YAML frontmatter and formatting issues |
| `/update-azure-skills` | Batch update Azure SDK-related skills |
| `/sync-web-app` | Sync skill data to web application |