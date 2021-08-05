# semantic-release-example
___
Inspired by [this article](https://schalkneethling.medium.com/automate-package-releases-with-semantic-release-and-commitizen-d7d4c337f04f)... and [this one](https://blog.logrocket.com/never-guess-about-project-history-again-31f65091f668/)

# Install 
Summary of changes required for implementation in this project

- run `npm i -g semantic-release-cli`
- run `semantic-release-cli setup`

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
