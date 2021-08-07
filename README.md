[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)
___
# semantic-release-example
Inspired by these articles
- [Automate package releases with semantic-release and commitizen](https://schalkneethling.medium.com/automate-package-releases-with-semantic-release-and-commitizen-d7d4c337f04f)
- [How to control your deployments and versioning with semantic-release & friends](https://blog.logrocket.com/never-guess-about-project-history-again-31f65091f668/)
- [Making commits the right way with hooks](https://dev.to/thelogicwarlock/making-commits-the-right-way-with-hooks-31h9)
- [How to lint git commit messages](https://remarkablemark.org/blog/2019/05/29/git-husky-commitlint/)

# Getting Started
This project demonstrates how to setup and configure semantic-release using [conventional commits](https://www.conventionalcommits.org/) and [commitizen](https://github.com/commitizen/cz-cli). 

Use `npm run cz` instead of `git commit` 
1. Install and configure semantic-release-cli
1. Commit messages

## Install
Summary of changes required for implementation in this project

- run `npm i -g semantic-release-cli`
- run `semantic-release-cli setup`
things
## npm-release.yml
This [github action](https://github.com/semantic-release/github/blob/4b902456b1c7958a59dca01bd3658dfde074f426/.github/workflows/release.yml) is  configured to run [manually](https://github.com/FreakinWard/semantic-release-example/blob/19f1bab239f3fc4d602f247747fe3ecc42dd9493/.github/workflows/npm-release.yml#L3) or with each [push](https://github.com/FreakinWard/semantic-release-example/blob/19f1bab239f3fc4d602f247747fe3ecc42dd9493/.github/workflows/npm-release.yml#L5) to `main`.

semantic-release-cli will need access to both the `github_token` [secret](https://docs.github.com/en/actions/reference/authentication-in-a-workflow) and `npm_token`.

1. Create a npm [publish token](https://docs.npmjs.com/creating-and-viewing-access-tokens)
1. Create a [github secret](https://docs.github.com/en/actions/reference/encrypted-secrets), named `NPM_TOKEN`
1. Pass  `GITHUB_TOKEN` and `NPM_TOKEN` as [Environment variables](https://github.com/semantic-release/github/blob/master/README.md#environment-variables)

## package.json
- Set `"version": "0.0.0-semantically-released"`
- Configure [repository url](https://github.com/semantic-release/semantic-release/blob/master/docs/usage/configuration.md#repositoryurl)

## .releaserc
Override default tag deployment, configure [branches](https://github.com/semantic-release/semantic-release/blob/master/docs/usage/configuration.md#branches) to trigger a release.

# Commit messages
[commitizen](https://github.com/commitizen/cz-cli) is used to create standard commit messages and is helpful using `git cli`

[commitlint](https://www.npmjs.com/package/@commitlint/cli) is used to lint the commit messages. This ensures that commit messages adhere to the standard format

IDE plugins are available as well
- [webstorm](https://plugins.jetbrains.com/plugin/9861-git-commit-template)
- [vscode](https://marketplace.visualstudio.com/items?itemName=KnisterPeter.vscode-commitizen)
- [visual studio](https://marketplace.visualstudio.com/items?itemName=mrluje.vs-commitizen)
