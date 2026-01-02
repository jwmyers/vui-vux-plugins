---
name: deploy
description: Deploy APK to Board hardware and launch the application
allowed-tools:
  - Bash
  - Read
argument-hint: "[apk-path]"
---

# Deploy to Board

Deploy and launch Zero-Day Attack on Board hardware using bdb (Board Developer Bridge).

## Process

1. Determine APK path:
   - Use provided path if specified
   - Default to `Builds/ZeroDayAttack.apk`

2. Install APK on Board:
   ```bash
   bdb install [apk-path]
   ```

3. Launch application:
   ```bash
   bdb launch com.earplay.zerodayattack
   ```

4. Optionally stream logs:
   ```bash
   bdb logs com.earplay.zerodayattack
   ```

## Commands Reference

| Command | Purpose |
|---------|---------|
| `bdb install [apk]` | Install APK to Board |
| `bdb launch [package]` | Launch application |
| `bdb logs [package]` | Stream application logs |
| `bdb stop [package]` | Stop application |

## Full Deployment

To install and launch in one command:
```bash
bdb install Builds/ZeroDayAttack.apk && bdb launch com.earplay.zerodayattack
```

## Troubleshooting

- If install fails, check bdb connection to device
- If launch fails, check package ID is correct
- If app crashes, run `bdb logs com.earplay.zerodayattack` to see errors
