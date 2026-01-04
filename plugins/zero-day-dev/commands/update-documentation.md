---
name: update-documentation
description: Update project documentation based on recent changes
allowed-tools: "*"
---

# Update Documentation

Update project documentation to reflect recent changes. This command coordinates documentation updates across CLAUDE.md, README.md, and skill reference files.

## Process

1. **Analyze Recent Changes**

   - Review what was modified
   - Identify affected documentation

2. **Update CLAUDE.md** (if architecture/build changed)

   - Script organization
   - Namespaces
   - Singleton managers
   - Build commands
   - Configuration

3. **Update README.md** (if user-facing changed)

   - Feature descriptions
   - Setup instructions
   - Usage examples

4. **Update Skill References** (if domain knowledge changed)

   - `zero-day-rules/references/` for game mechanics
   - `board-sdk/references/` for SDK patterns
   - `project-architecture/references/` for code architecture
   - `layout-sizing/references/` for layout math
   - `visual-style-guide/references/` for visual specs

5. **Update Plugin Components** (if workflows changed)

   - Skills (skills/\*/SKILL.md)
   - Agents (agents/\*.md)

6. **Verify Cross-References**
   - Check links between files
   - Ensure consistency

## Documentation Targets

| Target                             | Update When                                |
| ---------------------------------- | ------------------------------------------ |
| `CLAUDE.md`                        | Architecture, build, configuration changes |
| `README.md`                        | User-facing features change                |
| `zero-day-rules/references/`       | Game mechanics clarified                   |
| `board-sdk/references/`            | SDK usage patterns change                  |
| `project-architecture/references/` | Code architecture changes                  |
| `layout-sizing/references/`        | Layout/sizing changes                      |
| `visual-style-guide/references/`   | Visual specs change                        |

## Update Guidelines

**CLAUDE.md:**

- Keep concise - detail goes in skill references
- Focus on actionable information for AI
- Use tables for structured data
- Include code examples

**README.md:**

- User-friendly language
- Working commands
- Clear setup instructions

**Skill References:**

- Comprehensive domain knowledge
- Code examples and patterns
- Organized by topic

## Output

Provide summary of updates:

```text
## Documentation Update Summary

### Files Updated
- [file]: [changes]

### Cross-References Verified
- [status]

### Recommendations
- [any follow-up needed]
```

## Notes

- Maintain existing format and style
- Don't duplicate information across files
- Keep CLAUDE.md lean, detail in skill references
- Test any code examples included
