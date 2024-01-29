# Upgrade minor/patch version packages for node project

- This action use [npm-check-updates](https://www.npmjs.com/package/npm-check-updates) to update minor/patch version packages
- It will auto generate commit messages
- **_Note: Currently only support project using npm_**

## Usage

```yml
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

env:
  NODE_ENV: development
  COMMIT_MSG_BODY: ""
  GH_TOKEN: ${{ github.token }}

jobs:
  upgrade:
    name: Upgrade minor/patch version packages
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup node
        uses: actions/setup-node@v4
        with:
          node-version-file: .nvmrc

      - name: Upgrade minor/patch version packages
        uses: florencea/node-depsup-action@v1
```

## Development

```sh
# make new release
./make-tag
```
