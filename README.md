# @gravity-ui/package-example &middot; [![npm package](https://img.shields.io/npm/v/@gravity-ui/package-example)](https://www.npmjs.com/package/@gravity-ui/package-example) [![CI](https://img.shields.io/github/actions/workflow/status/gravity-ui/package-example/.github/workflows/ci.yml?label=CI&logo=github)](https://github.com/gravity-ui/package-example/actions/workflows/ci.yml?query=branch:main) [![storybook](https://img.shields.io/badge/Storybook-deployed-ff4685)](https://preview.gravity-ui.com/package-example/)

This is a template for a typical package.

## Repository setup

1. Create a new repository using this repository as a template.
2. Replace `package-example` throughout the repository with your package and repository name.
3. Complete the publishing setup below.
4. Adjust the remaining package settings as needed.

## Required publishing setup

The template already contains `.github/workflows/release.yml`. It creates releases with
`gravity-ui/release-action@v2` and publishes to npm in the same job through OpenID Connect (OIDC).
The release job uses Node.js 24 and grants `id-token: write`, so npm can obtain a short-lived publishing token.
Do not pass an npm token to the action or add a separate publishing job.

Complete these steps once for every repository created from the template:

1. Make sure the package already exists on npm. npm cannot configure a trusted publisher for an unpublished package;
   use the approved bootstrap publishing process for its first version.
2. In the GitHub repository, open **Settings → Environments**, create an environment named `npm-publish`, and set
   **Deployment branches and tags** to **Protected branches only**. Make sure `main` is protected in
   **Settings → Rules → Rulesets** or **Settings → Branches**; without branch protection, this setting allows any branch.
3. Make sure the organization secret `GRAVITY_UI_BOT_GITHUB_TOKEN` is available to the repository. It is used to
   create and update the release pull request; it is not used to publish to npm.
4. Use npm 11.15.0 or newer and an npm account that has write access to the package and account-level two-factor
   authentication enabled. Configure the trusted publisher:

```shell
npm trust github @gravity-ui/your-package \
  --repo gravity-ui/your-repository \
  --file release.yml \
  --env npm-publish \
  --allow-publish
```

The trusted publisher must reference this repository's `release.yml` workflow and match its `npm-publish` environment.

5. Verify the saved configuration:

```shell
npm trust list @gravity-ui/your-package
```

The result must contain the expected GitHub repository, `release.yml`, the `npm-publish` environment, and permission
to publish. After this setup, releases publish without `NPM_TOKEN` or `GRAVITY_UI_BOT_NPM_TOKEN`.

6. Merge a release pull request and check that the **Release** workflow succeeds and the new version appears on npm.
   The action creates the GitHub Release and runs `npm publish` once; npm obtains a short-lived token automatically.

Releases are skipped in the template repository itself and enabled in repositories created from it.

## Install

```shell
npm install --save-dev @gravity-ui/package-example
```

## Usage
