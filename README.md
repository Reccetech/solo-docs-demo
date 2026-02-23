# Solo Documentation

Standalone documentation site for Hiero Solo CLI.

## Overview

This repository contains the documentation website for [Hiero Solo](https://github.com/hiero-ledger/solo), a tool for deploying and managing Hiero Ledger Consensus Node Networks. The documentation is built using [Hugo](https://gohugo.io/) with the [Docsy](https://www.docsy.dev/) theme.

## Prerequisites

- **Hugo Extended** 0.145.0+ (installed via npm)
- **Go** 1.21+ (for Hugo modules)
- **Node.js** 22+ and npm

## Quick Start

### Install Dependencies

```bash
npm install
```

### Preview Locally

```bash
# Using npm
npm run preview

# Or using hugo directly
hugo server -D

# Or using task (if installed)
task
```

The site will be available at [http://localhost:1313/](http://localhost:1313/)

### Build for Production

```bash
# Using npm
npm run build

# Or using hugo directly
hugo --minify

# Or using task (if installed)
task build
```

The built site will be in the `public/` directory.

## Making Changes

1. Edit markdown files in `content/en/docs/` or `content/en/examples/`
2. Hugo will live-reload automatically when running `hugo server`
3. Preview your changes at http://localhost:1313/
4. Commit and push your changes

## Repository Structure

```
solo-docs/
├── content/en/          # Documentation content
│   ├── docs/           # User guides and documentation
│   │   ├── step-by-step-guide.md (template)
│   │   ├── advanced-deployments.md (template)
│   │   ├── solo-commands.md (to be generated)
│   │   └── ...
│   ├── examples/       # Example configurations
│   └── templates/      # Content templates (for reference)
├── layouts/            # Custom Hugo templates
├── assets/            # SCSS, images, icons
├── static/            # Static assets
├── examples/          # Raw example files (Taskfiles, configs)
├── hugo.yaml          # Hugo configuration
├── go.mod, go.sum    # Hugo module dependencies
├── package.json       # Node.js dependencies
└── Taskfile.yaml      # Task runner commands
```

## Content Generation

Some documentation pages are generated from Solo CLI commands and need to be created before the site can be fully built:

- `content/en/docs/step-by-step-guide.md` - Generated from `templates/step-by-step-guide.template.md`
- `content/en/docs/advanced-deployments.md` - Generated from `templates/advanced-deployments.template.md`
- `content/en/docs/solo-commands.md` - Generated from `solo --help` output
- `static/classes/` - API documentation (TypeDoc output)

**Note:** Content generation requires the Solo CLI codebase. For now, these files need to be generated manually from the main Solo repository before deploying this standalone docs site.

## Published Site

The documentation is published at: **https://solo.hiero.org/**

## Contributing

Contributions are welcome! To contribute:

1. Fork this repository
2. Create a feature branch
3. Make your changes
4. Test locally with `npm run preview`
5. Submit a pull request

For larger changes, please open an issue first to discuss the proposed changes.

## License

Apache License 2.0 - See [LICENSE](../LICENSE) in the Solo repository.

## Related Repositories

- [Hiero Solo](https://github.com/hiero-ledger/solo) - The main Solo CLI tool
- [Hiero Platform](https://github.com/hiero-ledger/hiero) - Hiero Ledger platform

## Support

- [Discord](https://discord.com/channels/905194001349627914/1364886813017247775) - `#solo` channel
- [GitHub Issues](https://github.com/hiero-ledger/solo/issues) - Bug reports and feature requests
- [Documentation](https://solo.hiero.org/) - User guides and API reference
