[![Latest Release](https://img.shields.io/github/v/release/mabioca/flarum-rtl-patch)](https://github.com/mabioca/flarum-rtl-patch/releases)

# Flarum RTL Patch for Flarum 2

A compatibility patch for improving RTL (Right-to-Left) asset compilation with Flarum 2 and `irmmr/flarum-ext-rtl`.

This project provides a compatibility fix for the Flarum 2 LESS asset compiler integration used by the RTL extension.

## About

Flarum 2 introduced changes to the frontend asset compilation pipeline.

During testing with `irmmr/flarum-ext-rtl`, the extension's LESS compiler override was found to be incompatible with the Flarum 2 compiler API.

In particular, the override did not contain some methods used by the Flarum 2 asset pipeline, such as:

- `setFontsDir()`
- `readCache()`
- `writeCache()`
- `pruneCacheOnce()`
- `fontRevision()`

This patch keeps the Flarum 2-compatible compiler implementation and adds the RTL-specific processing required by the extension.

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
- Supports Flarum 2 asset publishing workflow

## Installation

> ⚠️ This is not a Flarum extension and should not be installed as one.
>
> It is a compatibility patch for `irmmr/flarum-ext-rtl` on Flarum 2.

Before applying the patch, create a backup of your Flarum installation.

Clone the repository in a temporary directory:

```bash
cd /tmp
git clone https://github.com/mabioca/flarum-rtl-patch.git
cd flarum-rtl-patch
git checkout v1.0.1-flarum2
```

Go to the root directory of your Flarum installation before applying the patch.

Back up the existing RTL compiler override:

```bash
cp vendor/irmmr/flarum-ext-rtl/src/Overrides/Frontend/Compiler/LessCompiler.php \
   vendor/irmmr/flarum-ext-rtl/src/Overrides/Frontend/Compiler/LessCompiler.php.before-patch
```

Copy the patched compiler:

```bash
cp /tmp/flarum-rtl-patch/src/Overrides/Frontend/Compiler/LessCompiler.php \
   vendor/irmmr/flarum-ext-rtl/src/Overrides/Frontend/Compiler/LessCompiler.php
```

Then clear the Flarum cache:

```bash
php flarum cache:clear
```

If required, rebuild/publish the assets:

```bash
php flarum assets:publish
```

After applying the patch, enable `irmmr/flarum-ext-rtl` and verify that the forum and administration interface load correctly.

The generated assets should include:

```text
forum.rtl.css
admin.rtl.css
```

## Files

Main changes:
```text
src/Overrides/Frontend/Compiler/LessCompiler.php
composer.json
```

## Notes

This project is an unofficial compatibility patch.

It is not an official Flarum core change and is not an official replacement for `irmmr/flarum-ext-rtl`.

The patch has been tested against Flarum 2.0.0 RC8. Other Flarum 2 versions may require additional changes.

Always test the patch on a staging environment and keep a backup before applying it to a production forum.

## Credits

Original RTL implementation:

[irmmr/flarum-ext-rtl](https://github.com/irmmr/flarum-ext-rtl)

Flarum:

[Flarum](https://github.com/flarum/flarum)
