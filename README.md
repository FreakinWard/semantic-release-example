Simple demo of setting up semantic release, commitizen and husky

[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)
___
# semantic-release-example

# Inspired by
- [Writing meaningful commit messages](https://reflectoring.io/meaningful-commit-messages/)
- [Automate package releases with semantic-release and commitizen](https://schalkneethling.medium.com/automate-package-releases-with-semantic-release-and-commitizen-d7d4c337f04f)
- [How to control your deployments and versioning with semantic-release & friends](https://blog.logrocket.com/never-guess-about-project-history-again-31f65091f668/)
- [Making commits the right way with hooks](https://dev.to/thelogicwarlock/making-commits-the-right-way-with-hooks-31h9)
- [How to lint git commit messages](https://remarkablemark.org/blog/2019/05/29/git-husky-commitlint/)

# Getting Started
This project demonstrates how to configure [semantic-release](https://github.com/semantic-release/semantic-release) using [conventional commits](https://www.conventionalcommits.org/) and [commitizen](https://github.com/commitizen/cz-cli). 

1. [Setup semantic-release](#setup-semantic-release)
1. [Setup husky](#setup-husky)
1. [Setup commitizen](#setup-commitizen)
1. [Setup commitlint](#setup-commitlint)
1. [Setup github action](#setup-github-action)
1. [Plugins](#plugins)

# Setup semantic-release
Install and setup semantic release
1. Create a npm [publish token](https://docs.npmjs.com/creating-and-viewing-access-tokens) then save it as a [github secret](https://docs.github.com/en/actions/reference/encrypted-secrets), named `NPM_TOKEN`
   - This will be used later with [setup github action](#setup-github-action) step
1. `npm i -D semantic-release-cli`
1. `semantic-release-cli setup --npm-username={npmUserName} --npm-token={npmToken} --gh-token={githubToken}`
1. Commit current changes. Next step requires package.json to be free of any changes. 
1. `npm version '0.0.0-semantically-released'`

> NOTE: `npm version` will create a version tag and commit the changes.

```json5
// create .releaserc in root directory - this overrides default tag deployment
{
   "branches": ["main"]
}
```

[more details](https://schalkneethling.medium.com/automate-package-releases-with-semantic-release-and-commitizen-d7d4c337f04f#493d)

# Setup husky
> NOTE: `npm set-scripts` works with npm 7.x+

Install husky, create prepare script which installs husky
1. `npm i -D husky`
1. `npm set-script prepare "husky install"`
1. `npm run prepare`

# Setup commitizen
1. `npm i -D commitizen cz-conventional-changelog`
1. `commitizen init cz-conventional-changelog`
1. `npm set-script pre-commit "exec < /dev/tty && git cz --hook || true\n"`
1. `npx husky add .husky/pre-commit "npm run pre-commit" && git add .husky/pre-commit`

[more details](https://schalkneethling.medium.com/automate-package-releases-with-semantic-release-and-commitizen-d7d4c337f04f#4f24)

# Setup commitlint
1. `npm i -D @commitlint/{cli,config-conventional}`
1. `npm set-script commit-msg "npx --no-install commitlint --edit $1"`
1. `npx husky add .husky/commit-msg "npm run commit-msg" && git add .husky/commit-msg`

```javascript
// create commitlint.config.js in root directory
module.exports = {
    extends: ['@commitlint/config-conventional'],
};
```

# Setup github action
This [github action](https://github.com/semantic-release/github/blob/4b902456b1c7958a59dca01bd3658dfde074f426/.github/workflows/release.yml) is  configured to run manually or with each push to `main`.

> NOTE: This depends on NPM_TOKEN from [setup-semantic-release](#setup-semantic-release) step above

```yaml
// create .github/workflows/npm-release.yml
name: npm-release
on:
   workflow_dispatch:
   push:
      branches: [ main ]
jobs:
   release:
      runs-on: ubuntu-latest
      steps:
         - uses: actions/checkout@v2
         - uses: actions/setup-node@v1
           with:
              node-version: '12'
         - name: Install dependencies
           run: npm ci
         - name: Release
           env:
              NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
              GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
           run: npx semantic-release
```

# Plugins

- [webstorm](https://plugins.jetbrains.com/plugin/9861-git-commit-template)
- [vscode](https://marketplace.visualstudio.com/items?itemName=KnisterPeter.vscode-commitizen)
- [visual studio](https://marketplace.visualstudio.com/items?itemName=mrluje.vs-commitizen)
