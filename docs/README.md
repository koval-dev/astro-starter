# Astro Starter Documentation

Welcome to the documentation for the Astro Starter project. This guide covers all the components and features available in this starter template.

## 📚 Documentation Structure

```
docs/
├── README.md              # This file - main documentation index
├── coding-standards.md    # UI conventions and verification
├── color-guidelines.md    # Color usage guide
├── components/            # Component documentation
│   └── footer.md          # Footer component documentation
└── getting-started.md     # Getting started guide
```

## 🧩 Components

### UI Components

- **[Footer Component](./components/footer.md)** - Reusable footer with customizable company information
- **Button Component** - Coming soon
- **Navigation Component** - Coming soon

### Layout Components

- **Layout Component** - Coming soon
- **SEO Component** - Coming soon

## 🚀 Getting Started

See the [Getting Started Guide](./getting-started.md) for instructions on how to use this starter template.

## 🎨 Design System

This starter includes a comprehensive design system with:

- **Typography** - Semantic text classes (`text-h1`, `text-small`, etc.)
- **Colors** - OKLCH color tokens (`primary`, `accent`, `secondary`)
- **Spacing** - Consistent spacing utilities
- **Components** - Reusable UI components

## 📝 Contributing

When adding new components to this starter:

1. Read the [UI conventions](./coding-standards.md).
2. Create the component in `src/components/`, reusing shared prop contracts
   from `src/types/` where applicable.
3. Create documentation for its public API in `docs/components/`.
4. Update this index with links to new documentation.

Shared AI instructions live in [AGENTS.md](../AGENTS.md). Keep tool-specific
entry points focused on that file.

## 🔗 Quick Links

- [Project README](../README.md) - Main project overview
- [UI Conventions](./coding-standards.md) - Component, styling, and verification rules
- [Color Guidelines](./color-guidelines.md) - Color token usage
- [Source Code](../src/) - Component source files
- [Type Definitions](../src/types/) - TypeScript interfaces
