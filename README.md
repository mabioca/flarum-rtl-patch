# Flarum RTL Patch for Flarum 2

A compatibility patch for improving RTL (Right-to-Left) asset compilation in Flarum 2.

This project provides fixes for RTL CSS generation and LESS asset compilation issues when using RTL support with Flarum 2.

## About

Flarum has excellent support for extensions, but the asset compilation pipeline changed significantly in Flarum 2.

This patch improves compatibility between:

- Flarum 2 asset compiler
- `irmmr/flarum-ext-rtl`
- RTL CSS generation
- LESS compilation

The main goal is to generate RTL CSS sidecar assets correctly without breaking the default LTR assets.

## Problem

During migration to Flarum 2, RTL compilation could fail because of changes in:

- Frontend asset pipeline
- LESS compiler integration
- CSS compilation flow
- Asset publishing process

This patch adapts the compiler behavior for Flarum 2.

## Compatibility

Tested with:

| Component | Version |
|---|---|
| Flarum | 2.0.0-rc.8 |
| PHP | 8.5+ |
| MariaDB | 11.x |
| irmmr/flarum-ext-rtl | dev-main |

## Features

- Generates RTL CSS assets alongside normal CSS assets
- Keeps original LTR assets unchanged
- Improves LESS compiler compatibility
- Adds safer LESS cache handling
- Supports Flarum 2 asset publishing workflow

## Installation

This patch is intended for developers and advanced Flarum administrators.

Clone the repository:
```bash
git clone https://github.com/mabioca/flarum-rtl-patch.git
```

Copy the patched files into your Flarum installation.

After applying the patch:
```bash
php flarum assets:publish 
php flarum cache:clear
```

## Files Modified

Main changes:
```text
src/Overrides/Frontend/Compiler/LessCompiler.php
composer.json
```

## Notes

This project is a compatibility patch and is not an official Flarum extension.

Always test on a staging environment before applying it to a production forum.

## Credits

Original RTL implementation:

https://github.com/irmmr/flarum-ext-rtl

Flarum:

https://github.com/flarum/flarum
