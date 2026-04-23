# Theme Documentation

This document explains the theming system, how to customize colors, typography, and component styling.

## Theme Tokens
- Colors: primary, secondary, background, surface, text, muted
- Typography: font-family, font-size scale, line-height, weight
- Spacing: scale for margins/padding

## Customizing Theme
- Modify the theme variables in src/styles/theme.css (or equivalent).
- To switch themes at runtime, implement a ThemeProvider/store and apply CSS variables accordingly.

## Accessibility Considerations
- Ensure sufficient color contrast and focus outlines for interactive elements.
- Maintain semantic HTML and ARIA labels where required.
