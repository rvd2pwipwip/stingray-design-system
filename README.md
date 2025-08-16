# Stingray Design Tokens

This repository contains the design tokens used across Stingray applications. It serves as the single source of truth for design tokens in the form of CSS variables.

## Installation

```bash
npm install @stingray/design-tokens
```

## Usage

Import the CSS variables in your project:

```css
@import "@stingray/design-tokens/dist/primitives.css";
```

## Development

1. Clone the repository
2. Install dependencies: `npm install`
3. Make changes to tokens in the `tokens/` directory
4. Build: `npm run build`
5. View tokens: `npm run viewer` (opens visual token reference)

## Token Viewer

The project includes a visual token viewer (`token-viewer.html`) that shows:

- All color tokens with live swatches
- All typography styles with samples
- Interactive font family testing
- Typography primitives reference

Open it with `npm run viewer` or by opening `token-viewer.html` in your browser after building.

## Structure

- `tokens/primitives/` - Contains the primitive token definitions
  - `colors.json` - Base color palette and alpha variants
  - `typography-primitives.json` - Font families, sizes, weights, line heights
- `tokens/semantic/` - Contains semantic token definitions
  - `text-styles.json` - Text styles that map to your Figma typography
- `dist/` - Contains the built CSS variables
  - `primitives.css` - Foundation tokens (colors, typography primitives)
  - `semantic.css` - Semantic tokens (text styles like h1, body1, etc.)
- `config.json` & `semantic.config.json` - Style Dictionary configurations

## License

ISC
