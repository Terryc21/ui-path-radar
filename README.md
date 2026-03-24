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

UI Path Radar is part of a 5-skill audit suite. Each skill finds different issues, and findings from one feed into the next via `.agents/ui-audit/` handoff files.

| Skill | Focus | GitHub |
|-------|-------|--------|
| **Data Model Radar** | Model layer: fields, serialization, relationships, migrations | [data-model-radar](https://github.com/Terryc21/data-model-radar) |
| **UI Path Radar** (this skill) | Navigation paths, dead ends, broken promises | [ui-path-radar](https://github.com/Terryc21/ui-path-radar) |
| **Roundtrip Radar** | Data safety, error handling, round-trip completeness | [roundtrip-radar](https://github.com/Terryc21/roundtrip-radar) |
| **UI Enhancer** | Visual quality, spacing, color accessibility, layout | [ui-enhancer](https://github.com/Terryc21/ui-enhancer) |
| **Capstone Radar** | Unified grading, ship/no-ship decision | [capstone-radar](https://github.com/Terryc21/capstone-radar) |

### How They Work Together

```
data-model-radar  -->  ui-path-radar  -->  roundtrip-radar
 (foundation)          (navigation)        (data flows)
                            |                   |
                            v                   v
                               ui-enhancer
                               (visual quality)
                                     |
                                     v
                              capstone-radar
                              (unified grade + ship/no-ship)
```

**Recommended audit order:**
1. **Data Model Radar** first — verify model definitions before auditing flows
2. **UI Path Radar** second — find all entry points and broken paths
3. **Roundtrip Radar** third — audit data flows behind those paths
4. **UI Enhancer** fourth — polish views after structural issues are fixed
5. **Capstone Radar** last — unified grade and ship/no-ship decision

Each skill writes a handoff YAML file to `.agents/ui-audit/` with findings relevant to the other skills. Skills read these handoffs on startup and incorporate them as suspects. If a companion skill isn't installed, the handoff file sits harmlessly until it is.

## License

MIT
