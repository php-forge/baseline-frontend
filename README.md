<!-- markdownlint-disable MD041 -->
<p align="center">
    <a href="https://github.com/php-forge/baseline-frontend" target="_blank">
        <img src="https://avatars.githubusercontent.com/u/103309199?s%25253D400%252526u%25253Dca3561c692f53ed7eb290d3bb226a2828741606f%252526v%25253D4" width="35%" alt="PHP Forge">
    </a>
    <h1 align="center">Baseline Frontend</h1>
    <br>
</p>
<!-- markdownlint-enable MD041 -->

<p align="center">
    <strong>Frontend baseline for PHP Forge</strong><br>
    <em>Prettier and stylelint configs shared via <code>yii2-extensions/scaffold</code>. Pair with <code>php-forge/baseline</code> for core PHP/editor/CI tooling.</em>
</p>

## System requirements

- [`PHP`](https://www.php.net/downloads) 8.3 or higher.
- [`Composer`](https://getcomposer.org/download/) for dependency management.

## Installation

```bash
composer require php-forge/baseline-frontend:^0.1 --dev
```

Or add the dependency manually to `composer.json`:

```json
{
    "require-dev": {
        "php-forge/baseline-frontend": "^0.1"
    }
}
```

Then run `composer update`.

## Scaffolded distribution

This package is a [`yii2-extensions/scaffold`](https://github.com/yii2-extensions/scaffold) provider for **frontend
formatting and linting metadata** (Prettier + stylelint). Templates live under `metadata/` and are mapped to consumer
roots via the `{from, to}` form in `scaffold.json`.

Opt in by allowing the plugin and listing this package as an authorised provider:

```bash
composer require yii2-extensions/scaffold:^0.1 --dev
```

```json
{
    "config": {
        "allow-plugins": {
            "yii2-extensions/scaffold": true
        }
    },
    "extra": {
        "scaffold": {
            "auto": false,
            "allowed-packages": ["php-forge/baseline-frontend"]
        }
    }
}
```

With `auto: false`, the plugin does not run on `composer install`; sync templates manually:

```bash
vendor/bin/scaffold reapply --provider=php-forge/baseline-frontend
vendor/bin/scaffold diff <file>
vendor/bin/scaffold status
```

### Files distributed

```text
.
├── .prettierrc.json                   # replace: Prettier formatting rules (tabWidth 4, yml/md overrides)
├── .prettierignore                    # replace: Paths Prettier should skip
├── .stylelintignore                   # replace: Paths stylelint should skip
├── .stylelintrc.json                  # replace: stylelint config (standard-scss)
└── .github
    └── linters
        └── .stylelintrc.json          # replace: stylelint config for CI (mirrors root)
```

> **Why two `.stylelintrc.json`?** Some projects invoke `stylelint --config .stylelintrc.json` (root), others use
> `stylelint --config .github/linters/.stylelintrc.json --config-basedir .` (as in `php-forge/debug-core`). This
> provider ships both targets from the same source so either invocation works after scaffold.

Mode semantics:

- `replace`: lock-step with this package. Local edits trigger a warning and the file is skipped on update.
- `append`: provider content is merged into the existing file; consumer additions never blown away.
- `preserve`: file is written once on first install and never overwritten.

## Related packages

For core PHP editor, git and generic linter configs, see [`php-forge/baseline`](https://github.com/php-forge/baseline).
For ECS and Rector configurations and their root wrapper templates, see
[`php-forge/coding-standard`](https://github.com/php-forge/coding-standard). The three packages are independent — adopt
any combination.

Install only `baseline` for pure PHP libraries. Add `baseline-frontend` in projects with JS/CSS/SCSS or where
`quality.yml` needs `prettier-config`/`prettier-ignore-path` (optional inputs):

```json
{
    "require-dev": {
        "php-forge/baseline": "^0.1",
        "php-forge/baseline-frontend": "^0.1",
        "php-forge/coding-standard": "^0.3",
        "yii2-extensions/scaffold": "^0.1"
    },
    "extra": {
        "scaffold": {
            "allowed-packages": [
                "php-forge/baseline",
                "php-forge/baseline-frontend",
                "php-forge/coding-standard"
            ]
        }
    }
}
```

Frontend `package.json` setup:

```json
{
    "devDependencies": {
        "prettier": "^3.9.6",
        "stylelint": "^17.14.1",
        "stylelint-config-standard-scss": "^17.0.0"
    },
    "scripts": {
        "format": "prettier --write 'resources/**/*.{js,css,scss}' 'docs/**/*.md' 'package.json'",
        "format:check": "prettier --check 'resources/**/*.{js,css,scss}' 'docs/**/*.md' 'package.json'",
        "lint:css": "stylelint --config .stylelintrc.json --config-basedir . 'resources/src/**/*.css'",
        "lint:css:fix": "stylelint --config .stylelintrc.json --config-basedir . --fix 'resources/src/**/*.css'"
    }
}
```

## Package information

[![PHP](https://img.shields.io/badge/%3E%3D8.3-777BB4.svg?style=for-the-badge&logo=php&logoColor=white)](https://www.php.net/releases/8.3/en.php)
[![Latest Stable Version](https://img.shields.io/packagist/v/php-forge/baseline-frontend.svg?style=for-the-badge&logo=packagist&logoColor=white&label=Stable)](https://packagist.org/packages/php-forge/baseline-frontend)
[![Total Downloads](https://img.shields.io/packagist/dt/php-forge/baseline-frontend.svg?style=for-the-badge&logo=composer&logoColor=white&label=Downloads)](https://packagist.org/packages/php-forge/baseline-frontend)

## Project status

[![Quality](https://img.shields.io/github/actions/workflow/status/php-forge/baseline-frontend/quality.yml?style=for-the-badge&label=Quality&logo=github)](https://github.com/php-forge/baseline-frontend/actions/workflows/quality.yml)
[![Security](https://img.shields.io/github/actions/workflow/status/php-forge/baseline-frontend/security.yml?style=for-the-badge&label=Security&logo=github)](https://github.com/php-forge/baseline-frontend/actions/workflows/security.yml)
[![StyleCI](https://img.shields.io/badge/StyleCI-Passed-44CC11.svg?style=for-the-badge&logo=github&logoColor=white)](https://github.styleci.io/repos/php-forge/baseline-frontend?branch=main)

## Our social networks

[![Follow on X](https://img.shields.io/badge/-Follow%20on%20X-1DA1F2.svg?style=for-the-badge&logo=x&logoColor=white&labelColor=000000)](https://x.com/Terabytesoftw)

## License

[![License](https://img.shields.io/badge/License-BSD--3--Clause-brightgreen.svg?style=for-the-badge&logo=opensourceinitiative&logoColor=white&labelColor=555555)](LICENSE)
