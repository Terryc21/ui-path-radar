# UI Path Radar

> 5-layer UI path audit for SwiftUI/UIKit apps. Discovers entry points, traces flows, detects dead ends and broken promises, evaluates UX impact, and verifies data wiring.

## What It Does

UI Path Radar systematically walks every button, link, menu item, and navigation path in your app to verify they all work. It finds:

- **Dead ends** — buttons that do nothing
- **Broken promises** — "Export PDF" opens the wrong screen
- **Orphaned views** — views that exist but can't be reached
- **Platform gaps** — works on iOS but broken on macOS
- **Missing feedback** — actions complete with no confirmation

## Quick Start

```
/ui-path-radar              # Full 5-layer audit
/ui-path-radar layer1       # Discovery only
/ui-path-radar layer2       # Flow tracing
/ui-path-radar layer3       # Issue detection
/ui-path-radar trace "Dashboard -> Add Item -> Save"
```

## Installation

Copy `SKILL.md` to `~/.claude/skills/ui-path-radar/SKILL.md`

## Companion Skills

UI Path Radar is part of a 4-skill audit suite. Each skill finds different issues, and findings from one feed into the next via `.agents/ui-audit/` handoff files.

| Skill | Focus | GitHub |
|-------|-------|--------|
| **UI Path Radar** (this skill) | Navigation paths, dead ends, broken promises | [ui-path-radar](https://github.com/Terryc21/ui-path-radar) |
| **Roundtrip Radar** | Data safety, error handling, round-trip completeness | [roundtrip-radar](https://github.com/Terryc21/roundtrip-radar) |
| **UI Enhancer** | Visual quality, spacing, color accessibility, layout | [ui-enhancer](https://github.com/Terryc21/ui-enhancer) |
| **Release Ready Radar** | Ship readiness, A-F grading across 24 domains | [release-ready-radar](https://github.com/Terryc21/release-ready-radar) |

### How They Work Together

```
ui-path-radar  -->  roundtrip-radar  -->  release-ready-radar
 (navigation)       (data safety)         (ship/no-ship)
      |                   |
      v                   v
         ui-enhancer
         (visual quality)
```

**Recommended audit order:**
1. **UI Path Radar** first — find all entry points and broken paths
2. **Roundtrip Radar** second — audit data flows behind those paths
3. **UI Enhancer** third — polish views after structural issues are fixed
4. **Release Ready Radar** last — final ship/no-ship grade

Each skill writes a handoff YAML file to `.agents/ui-audit/` with findings relevant to the other skills. Skills read these handoffs on startup and incorporate them as suspects. If a companion skill isn't installed, the handoff file sits harmlessly until it is.

## License

MIT
