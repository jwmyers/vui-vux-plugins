---
name: test
description: Run Unity tests via MCP
allowed-tools:
  - mcp__ai-game-developer__tests-run
  - Read
argument-hint: "[EditMode|PlayMode] [test-class]"
---

# Run Tests

Execute Unity tests using the Unity MCP tests-run tool.

## Process

1. Parse arguments:
   - First arg: Test mode (EditMode or PlayMode, default: EditMode)
   - Second arg: Optional test class name filter

2. Run tests via MCP:
   ```json
   {
     "testMode": "[EditMode|PlayMode]",
     "testClass": "[optional-class]",
     "includePassingTests": false,
     "includeMessages": true
   }
   ```

3. Report results:
   - Total tests, passed, failed
   - Details of any failures

## Test Modes

**EditMode** (default):
- Runs without Play mode
- Fast execution
- Tests pure logic and data

**PlayMode**:
- Runs in simulated Play mode
- Tests runtime behavior
- Requires scene setup

## Examples

Run all EditMode tests:
```
/test
```

Run all PlayMode tests:
```
/test PlayMode
```

Run specific test class:
```
/test EditMode LayoutConfigTests
```

## Existing Tests

| Test File | Mode | Tests |
|-----------|------|-------|
| BoardLayoutConfigTests | Editor | LayoutConfig values |
| TileDatabaseTests | Editor | Database integrity |
| CoordinateConversionTests | Runtime | Coordinate conversion |
| GameInitializationTests | Runtime | Game startup |

## Notes

- MCP connection must be active
- Unity Editor must be open
- Check Unity Console for additional context on failures
