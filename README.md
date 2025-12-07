# My Advent of CALM Journey

This repository tracks my 24-day journey learning the Common Architecture Language Model (CALM).

## Progress

- [x] Day 1: Install CALM CLI and Initialize Repository
- [x] Day 2: Create Your First Node
- [x] Day 3: Connect Nodes with Relationships
- [x] Day 4: Install CALM VSCode Extension
...

## Tools

### CALM CLI (Day 1)

The CALM Command Line Interface provides essential tooling for working with CALM architectures locally.

**What it's used for:**
- **Generation** – Create new architecture files and templates
- **Validation** – Verify your CALM models conform to the schema
- **Templates** – Bootstrap new architectures with pre-built structures

**Basic commands:**
```bash
calm init              # Initialize a new CALM project
calm validate          # Validate your architecture files
calm generate          # Generate documentation from models
```

### CALM VSCode Extension (Day 4)

The CALM extension brings architecture visualization and navigation directly into your editor.

**Installation:**
- [FINOS CALM VSCode Plugin](https://marketplace.visualstudio.com/items?itemName=FINOS.calm-vscode-plugin)

**What it provides:**
- **Visualization** – Visual diagrams of your architecture nodes and relationships
- **Tree Navigation** – Browse architecture components in a structured tree view
- **Live Preview** – See changes reflected in real-time as you edit

**Keyboard shortcut:**
- Press `Ctrl+Shift+C` (Windows/Linux) or `Cmd+Shift+C` (Mac) to open the preview panel

### How They Work Together

The CLI and VSCode extension are complementary tools in your CALM workflow:

- **CLI** handles validation and ensuring your architectures conform to the CALM schema
- **Extension** provides visual feedback and interactive exploration of your models
- Together, they enable a complete development experience: write and validate with the CLI, visualize and refine with the extension

## Architectures

This directory will contain CALM architecture files documenting systems.

## Patterns

This directory will contain CALM patterns for architectural governance.

## Docs

Generated documentation from CALM models.