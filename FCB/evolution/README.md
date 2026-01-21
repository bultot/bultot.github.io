# Backbase Evolution Timeline

An interactive visualization showing the evolution of Backbase's platform architecture from 2011 to 2026.

## Overview

This single-page application presents the history of Backbase's product evolution through an animated, scrollable timeline. As users scroll through the years, the architecture diagram on the right updates to show which components existed at each point in time.

## Features

- **Interactive Timeline**: Scroll through years 2011-2026 to see how the platform evolved
- **Animated Architecture Diagram**: Components appear, resize, and highlight as you progress
- **"New Block" Highlighting**: Newly appearing components get a teal/cyan glow effect
- **Auto-play Mode**: Click "Play Story" to auto-scroll through the timeline
- **Responsive Layout**: Timeline on left, sticky architecture diagram on right

## Technology Stack

- **React 18** (via CDN, no build step required)
- **Babel** (in-browser JSX transpilation)
- **Tailwind CSS** (via CDN)
- **Vanilla JavaScript** for scroll handling and animations

## Architecture Layers

The diagram visualizes these platform layers:

| Layer | Description |
|-------|-------------|
| Presentation Services | UI components, Model Bank Apps, AI Co-Pilots |
| Banking Services | Core banking functionality, Omni-Banking Services |
| Process Automation | Flow orchestration engine |
| Agentic Services | Agent Studio for AI agents |
| Semantic Services | NEXUS Customer State Graph |
| Integration Services | Grand Central integration hub |
| Marketplace | Connector Studio |
| Entitlements Services | Access Control (vertical pillar) |
| Security Services | Identity management (vertical pillar) |
| Cloud Infrastructure | BaaS platform |
| Agentic SDLC | AI-powered DevOps toolchain |

## Channel & LOB Tracking

The top section tracks:

**Self-Service Channels:**
- Web
- Mobile

**Assisted Channels:**
- Branch
- Call Center
- Relationship Manager
- Back Office

**Lines of Business:**
- Retail
- SME
- Commercial
- Wealth

## Timeline Data Structure

Each year entry contains:

```javascript
{
    year: 2024,
    era: "AI-Native Era",
    title: "Agentic Services",
    marketAsk: "What the market requested",
    strategicImpact: "Business impact of the response",
    response: "Backbase's product response",
    description: "Detailed explanation",
    channels: { web: true, mobile: true, branch: true, callCenter: true },
    frontline: { retail: true, sme: true, commercial: true, wealth: true, rm: true, backOffice: true },
    arch: {
        presentation: { status: 'active', sub: "AI Co-Pilots", highlight: false },
        // ... other layers
    }
}
```

## Layer States

- `hidden`: Layer not yet introduced (collapsed, invisible)
- `active`: Layer exists and is functional
- `incubation`: Layer in development (dashed border)
- `highlight`: Featured layer for this year (cyan accent)

## "New" Highlighting Logic

Components are highlighted as "new" when they transition from inactive to active compared to the previous year:

```javascript
const isNewArch = (key) => {
    if (!prevData) return activeData.arch[key].status === 'active';
    return activeData.arch[key].status === 'active' && prevData.arch[key].status !== 'active';
};
```

New items receive:
- Teal background (`#0A4D5C`)
- Cyan border (`#00D4FF`)
- Glow effect (`shadow-[0_0_16px_rgba(0,212,255,0.35)]`)

## Local Development

No build step required. Simply open `index.html` in a browser:

```bash
open index.html
# or
python -m http.server 8000
```

## File Structure

```
evolution/
├── index.html      # Single-file React application
├── README.md       # This file
└── CLAUDE.md       # AI assistant reference
```

## Customization

### Adding a New Year

1. Add a new entry to the `timelineData` array
2. Set appropriate `channels`, `frontline`, and `arch` states
3. Use `highlight: true` on the featured layer for that year

### Modifying Styles

- Backbase brand colors are defined in CSS variables (`:root`)
- Component styles use Tailwind CSS classes
- Animation timing uses `cubic-bezier(0.625, 0.05, 0, 1)`

## Browser Support

Modern browsers with ES6+ support:
- Chrome 80+
- Firefox 75+
- Safari 13+
- Edge 80+
