# Upgrade minor/patch version packages for node project

- This action use [npm-check-updates](https://www.npmjs.com/package/npm-check-updates) to update minor/patch version packages
- It will update `package.json`, `package-lock.json` and auto generate commit messages
- **_Note: Currently only support project using npm_**

## Usage

```yaml
name: Upgrade

on:
  # GitHub Actions use UTC time, so 20:00 means 4:00 UTC +8 Timezone
  schedule:
    - cron: "0 20 * * *"
  workflow_dispatch:

permissions:
  contents: write
  actions: read
  checks: write

jobs:
  upgrade:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version-file: .nvmrc
          cache: npm
      - uses: florencea/node-depsup-action@v1
```

## Development

```sh
# make new release
./make-tag
```
