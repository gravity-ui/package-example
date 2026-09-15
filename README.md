# @gravity-ui/package-example &middot; [![npm package](https://img.shields.io/npm/v/@gravity-ui/package-example)](https://www.npmjs.com/package/@gravity-ui/package-example) [![CI](https://img.shields.io/github/actions/workflow/status/gravity-ui/package-example/.github/workflows/ci.yml?label=CI&logo=github)](https://github.com/gravity-ui/package-example/actions/workflows/ci.yml?query=branch:main) [![storybook](https://img.shields.io/badge/Storybook-deployed-ff4685)](https://preview.gravity-ui.com/package-example/)

This is a template for a typical package.

1. Create a new repository and use this repository as a template.
2. Replace `package-example` through the whole repository with your name.
3. Configure npm trusted publishing as described below.
4. Overwrite other things at your desire.

## Publishing setup

The release workflow publishes through OpenID Connect and does not require an npm token.

1. Make sure the package already exists on npm. Creating a trusted publisher for a package that has not been
   published yet is not supported.
2. Create a GitHub Environment named `npm-publish` and restrict its deployment branches to protected branches.
3. With npm 11.15.0 or newer, configure the package's trusted publisher once:

```shell
npm trust github @gravity-ui/your-package \
  --repo gravity-ui/your-repository \
  --file release.yml \
  --env npm-publish \
  --allow-publish
```

The npm account running this command must have write access to the package and two-factor authentication enabled.
The `GRAVITY_UI_BOT_GITHUB_TOKEN` organization secret must be available to the repository so that the release action
can create and update the release pull request.

## Install

```shell
npm install --save-dev @gravity-ui/package-example
```

## Usage
