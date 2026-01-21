# Claude Code Reference - Backbase Evolution Timeline

## Project Summary

Interactive timeline visualization of Backbase platform evolution (2011-2026). Single HTML file with React, Babel, and Tailwind CSS loaded via CDN.

## Key File

- `index.html` - Contains everything: React components, timeline data, styles

## Architecture

### Components (in index.html)

| Component | Purpose |
|-----------|---------|
| `App` | Main component, manages state and scroll handling |
| `TimelineItem` | Individual year entry with intersection observer |
| `ArchitectureLayer` | Horizontal layer box (Presentation, Banking, etc.) |
| `VerticalArchitectureLayer` | Vertical pillar (Entitlements, Security) |
| `ChannelBadge` | Channel/LOB badge (Web, Mobile, Retail, etc.) |
| `FrontlineBadge` | Legacy badge component (still used for some items) |

### Data Structure

`timelineData` array at line ~213 contains all year entries. Each entry has:

```javascript
{
    year: number,
    era: string,           // "Bank 2.0 Portal Era", "CXP Era", etc.
    title: string,
    marketAsk: string,     // Customer need
    strategicImpact: string,
    response: string,      // Backbase's answer
    description: string,
    channels: {
        web: boolean,
        mobile: boolean,
        branch: boolean,
        callCenter: boolean
    },
    frontline: {
        retail: boolean,
        sme: boolean,
        commercial: boolean,
        wealth: boolean,
        rm: boolean,
        backOffice: boolean
    },
    arch: {
        presentation: { status: string, sub: string, highlight?: boolean },
        banking: { ... },
        automation: { ... },
        agentic: { ... },
        semantic: { ... },
        integration: { ... },
        marketplace: { ... },
        entitlements: { ... },
        security: { ... },
        cloudInfra: { ... },
        agenticSdlc: { ... }
    }
}
```

### Layer Status Values

- `'hidden'` - Not visible, collapsed
- `'active'` - Visible and styled
- `'incubation'` - Dashed border, in development

### "New" Highlighting System

Helper functions compare current year with previous year:

```javascript
const getPreviousYearData = (currentYear) => { ... }
const isNewChannel = (key) => { ... }
const isNewFrontline = (key) => { ... }
const isNewArch = (key) => { ... }
```

New items get teal background (`#0A4D5C`) with cyan glow.

## Brand Colors (CSS Variables)

```css
--bb-navy: #041E42;      /* Primary */
--bb-blue: #0066FF;      /* Electric Blue */
--bb-cyan: #00D4FF;      /* Accent */
```

## Common Tasks

### Add new timeline year

1. Find `timelineData` array (~line 213)
2. Copy an existing year entry
3. Update year, era, title, descriptions
4. Set `channels`, `frontline`, `arch` states
5. Set `highlight: true` on the key layer for that year

### Modify animation timing

Search for `cubic-bezier(0.625, 0.05, 0, 1)` - this is the standard Backbase easing.

### Change "new" highlight color

Search for `#0A4D5C` (teal background) and `#00D4FF` (cyan accents).

### Add new architecture layer

1. Add to `arch` object in all timeline entries
2. Create rendering in App component's architecture section
3. Pass `isNew={isNewArch('newLayerKey')}` prop

### Add new channel/LOB

1. Add to `channels` or `frontline` in all timeline entries
2. Add ChannelBadge in the appropriate section
3. Pass `isNew={isNewChannel('key')}` or `isNewFrontline('key')` prop

## Testing Changes

No build step - just refresh browser:

```bash
open index.html
```

## Timeline History Accuracy

Based on Backbase product history:

| Year | Key Additions |
|------|---------------|
| 2011 | Web, Presentation, Integration |
| 2013 | Mobile, Retail LOB |
| 2016 | Banking Services, Entitlements, Security |
| 2019 | SME, Process Automation |
| 2022 | Wealth, RM, Marketplace, BaaS |
| 2023 | Commercial, Branch, Call Center, Back Office, SDLC |
| 2024 | Agentic Services |
| 2025 | Agentic SDLC enhanced |
| 2026 | Semantic Services (NEXUS) |

## Gotchas

- Split layers (Integration/Marketplace, BaaS/SDLC) use conditional width classes
- Vertical pillars have rotated text via `writing-mode: vertical-rl`
- First year shows all active items as "new" (no previous year to compare)
- `highlight` prop shows the featured layer; `isNew` shows newly appeared layers
