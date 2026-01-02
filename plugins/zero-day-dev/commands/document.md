---
name: document
description: Update project documentation based on recent changes
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
---

# Update Documentation

Update project documentation to reflect recent changes. This command coordinates documentation updates across CLAUDE.md, README.md, and Documentation/ files.

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

4. **Update Documentation/** (if systems changed)
   - ARCHITECTURE-ANALYSIS.md
   - DIGITIZATION-ANALYSIS.md
   - Other technical docs

5. **Update Plugin Components** (if domain knowledge changed)
   - Skills (skills/*/SKILL.md)
   - Agents (agents/*.md)

6. **Verify Cross-References**
   - Check links between files
   - Ensure consistency

## Documentation Files

| File | Update When |
|------|-------------|
| `CLAUDE.md` | Architecture, build, configuration changes |
| `README.md` | User-facing features change |
| `Documentation/ARCHITECTURE-ANALYSIS.md` | Code architecture changes |
| `Documentation/DIGITIZATION-ANALYSIS.md` | Implementation changes |
| `Documentation/RULES-ANALYSIS.md` | Game mechanics clarified |

## Update Guidelines

**CLAUDE.md:**
- Keep concise - detail goes in Documentation/
- Focus on actionable information for AI
- Use tables for structured data
- Include code examples

**README.md:**
- User-friendly language
- Working commands
- Clear setup instructions

**Documentation/:**
- Comprehensive technical detail
- Code examples
- Architecture diagrams

## Output

Provide summary of updates:
```
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
- Keep CLAUDE.md lean, detail in Documentation/
- Test any code examples included
