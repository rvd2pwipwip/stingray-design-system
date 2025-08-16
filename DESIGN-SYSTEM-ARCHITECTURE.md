# Stingray Design System Architecture

**Version:** 1.0.0 (Early Development)  
**Last Updated:** August 15, 2025  
**Status:** 🚧 In Development

## Overview

The Stingray Design System is built on a hybrid token architecture that separates **UX consistency** from **brand flexibility**. This allows teams to maintain consistent user experience patterns while enabling flexible visual styling across different brands and applications.

## Core Philosophy

> **"Similar UX components with very flexible UI styling"**

- **UX Patterns** remain consistent across all applications
- **Visual Styling** can be customized per brand/project
- **Components** are brand-agnostic but UX-consistent
- **Tokens** provide both system-level and brand-level customization

## Architecture Overview

### Two-Layer Token System

```
┌─────────────────────────────────────────┐
│           CLIENT PROJECTS               │
│  ┌─────────────────┐ ┌─────────────────┐│
│  │  Music App      │ │  Karaoke App    ││
│  │  Brand Tokens   │ │  Brand Tokens   ││
│  │  Component      │ │  Component      ││
│  │  Overrides      │ │  Overrides      ││
│  └─────────────────┘ └─────────────────┘│
└─────────────────────────────────────────┘
                    ▲
                    │ consumes
                    ▼
┌─────────────────────────────────────────┐
│        STINGRAY-DESIGN-TOKENS           │
│  ┌─────────────────┐ ┌─────────────────┐│
│  │  Primitive      │ │  UX Semantic    ││
│  │  Colors         │ │  Tokens         ││
│  │  (Foundation)   │ │  (Behavior)     ││
│  └─────────────────┘ └─────────────────┘│
└─────────────────────────────────────────┘
```

## Token Layers

### Layer 1: Primitive Tokens (✅ Implemented)

**Location:** `stingray-design-tokens/tokens/primitives/`  
**Purpose:** Raw design values (colors, typography scales, spacing scales)  
**Consumers:** Semantic tokens, brand tokens  
**Update Frequency:** Rarely (when adding new primitives)

**Current Implementation:**

```css
--color-gray-050: #fafafa;
--color-gray-100: #f5f5f5;
--color-gray-900: #191919;
--color-stingray-500: #3b82f6;
--color-white: #ffffff;
--color-black: #000000;
/* Alpha variants */
--color-white-alpha-050: rgba(255, 255, 255, 0.05);
--color-black-alpha-950: rgba(25, 25, 25, 0.95);
```

### Layer 2: UX Semantic Tokens (🚧 Next Phase)

**Location:** `stingray-design-tokens/tokens/semantic/`  
**Purpose:** Functional design decisions (surface hierarchy, text hierarchy, interaction patterns)  
**Consumers:** Component library, client projects  
**Update Frequency:** Occasionally (when UX patterns evolve)

**Planned Implementation:**

```css
/* Surface Hierarchy */
--surface-base: var(--color-gray-050);
--surface-elevated: var(--color-white);
--surface-overlay: var(--color-white-alpha-900);

/* Text Hierarchy */
--text-primary: var(--color-gray-900);
--text-secondary: var(--color-gray-700);
--text-disabled: var(--color-gray-400);

/* Interaction States */
--interaction-hover-opacity: 0.8;
--interaction-focus-ring-width: 2px;
--interaction-disabled-opacity: 0.4;
```

### Layer 3: Brand/Component Tokens (🎯 Client Projects)

**Location:** `client-project/src/tokens/`  
**Purpose:** Brand-specific styling, component-specific overrides  
**Consumers:** React components, CSS  
**Update Frequency:** Often (brand iterations, A/B testing)

**Example Implementation:**

```css
/* Brand Tokens - Music App */
--brand-primary: var(--color-stingray-500);
--brand-accent: var(--color-blue-600);

/* Component Tokens */
--component-button-primary-bg: var(--brand-primary);
--component-button-primary-text: var(--color-white);
--component-card-border-radius: 8px;
```

## Design Decisions & Rationale

### Why Hybrid Architecture?

| Requirement           | Solution                        | Benefit                         |
| --------------------- | ------------------------------- | ------------------------------- |
| Similar UX components | UX semantic tokens in system    | Consistent behavior patterns    |
| Flexible UI styling   | Brand tokens in client projects | Easy brand customization        |
| Multi-brand support   | Separated concerns              | Independent brand iteration     |
| Team autonomy         | Clear token boundaries          | UI/Dev teams work independently |
| Best practices        | Hierarchical token structure    | Maintainable, scalable system   |

### Token Naming Conventions

**Format:** `[category]-[element]-[variant]-[state]`

**Examples:**

- `surface-primary` (main background)
- `text-primary` (primary text color)
- `component-button-primary-bg` (primary button background)
- `component-button-primary-bg-hover` (hover state)

**Rationale:**

- Clear hierarchy and purpose
- Works in both Figma and code
- Scales well for components
- Self-documenting for developers

## Implementation Strategy

### Phase 1: Foundation (✅ Complete)

- [x] Primitive color tokens from Figma
- [x] Style Dictionary build system
- [x] CSS variable generation
- [x] Package structure

### Phase 2: UX Semantics (🚧 Current)

- [ ] Core surface tokens (base, elevated, overlay)
- [ ] Text hierarchy tokens
- [ ] Interaction state tokens
- [ ] Basic spacing/sizing semantics

### Phase 3: Component Integration (🎯 Planned)

- [ ] Create basic components using UX semantics
- [ ] Test component brand flexibility
- [ ] Document component token patterns

### Phase 4: Brand Implementation (🎯 Planned)

- [ ] Music app brand token layer
- [ ] Karaoke app brand token layer
- [ ] Theme switching capabilities

## Usage Guidelines

### For UI/UX Designers

**Use Primitive Tokens When:**

- Defining new brand colors
- Creating color scales
- Working with foundational design elements

**Use UX Semantic Tokens When:**

- Designing component behaviors
- Defining interaction patterns
- Creating consistent surface hierarchies

**Use Brand Tokens When:**

- Customizing visual appearance
- Creating brand-specific variants
- A/B testing visual treatments

### For Developers

**Consume UX Semantic Tokens When:**

- Building reusable components
- Implementing consistent interaction patterns
- Need system-level consistency

**Consume Brand Tokens When:**

- Styling brand-specific elements
- Implementing visual customizations
- Building brand-aware components

**Never Directly Use:**

- Primitive tokens in components (use semantic layer)
- Hard-coded color values (always use tokens)

## Component Strategy

### Component Token Pattern

```tsx
// ✅ Good: Component uses semantic tokens
const Button = ({ variant = "primary" }) => (
  <button
    className={`button button--${variant}`}
    style={{
      backgroundColor: `var(--component-button-${variant}-bg)`,
      color: `var(--component-button-${variant}-text)`,
      // UX behavior from system
      opacity: "var(--interaction-hover-opacity)",
    }}
  >
    {children}
  </button>
);
```

### Brand Flexibility Example

```css
/* Music App */
.music-theme {
  --component-button-primary-bg: var(--color-stingray-500);
  --component-button-secondary-bg: var(--color-gray-100);
}

/* Karaoke App */
.karaoke-theme {
  --component-button-primary-bg: var(--color-purple-500);
  --component-button-secondary-bg: var(--color-pink-100);
}
```

## Future Considerations

### Multi-Theme Support

- Light/dark theme variants
- High contrast accessibility themes
- Seasonal or promotional themes

### Advanced Token Types

- Typography tokens (font families, sizes, line heights)
- Spacing tokens (margins, padding, gaps)
- Animation tokens (durations, easing functions)
- Shadow tokens (elevation system)

### Tooling Integration

- Figma token sync
- Design token documentation site
- Automated visual regression testing
- Token usage analytics

## Questions & Decisions Log

### Open Questions

- Should component-specific tokens live in the system or client projects?
- How granular should the UX semantic layer be?
- What's the migration strategy for existing projects?

### Decision History

- **2025-08-15:** Chose hybrid architecture over centralized semantics
- **2025-08-15:** Decided to separate UX patterns from brand styling
- **2025-08-15:** Established primitive tokens as foundation layer

---

## Contributing

This document should be updated as the design system evolves. When making architectural changes:

1. Document the decision and rationale
2. Update relevant examples
3. Consider impact on existing implementations
4. Communicate changes to all stakeholders

## Resources

- [Style Dictionary Documentation](https://amzn.github.io/style-dictionary/)
- [Design Token Specification](https://design-tokens.github.io/community-group/format/)
- [Token Naming Best Practices](https://spectrum.adobe.com/page/design-tokens/)

---

**Next Update:** After implementing UX semantic tokens (Phase 2)
