# study project for commit automation

[TOC]

#### 1 - Install commitLint ( https://commitlint.js.org/ )
`npm install -g @commitlint/cli @commitlint/config-conventional -D`

##### 1.1 - Configure commitlint to use conventional config:
`echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js`

#### 2 - Install husky ( https://github.com/typicode/husky )
`npm install husky -D`

##### 2.2 - Added husky to package.json
```javascript
{
...
  "husky": {
    "hooks": {
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
    }
  },
...
}
```

#### 3 - Install commitizen ( https://github.com/commitizen/cz-cli )
`npm install --global commitizen`

##### 3.1 - Run commitizen configuration inside your project
`commitizen init cz-conventional-changelog --save-dev --save-exact`

##### 3.2 - Add commitizen configuration for husky in package.json
```javascript
{
...
  "husky": {
    "hooks": {
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS",
      "prepare-commit-msg": "/dev/tty && git cz --hook || true"
    }
  },
...
}
```

#### IDE plugins
Microsoft Visual Studio Code
https://marketplace.visualstudio.com/items?itemName=KnisterPeter.vscode-commitizen

JetBrains WebStorm
https://plugins.jetbrains.com/plugin/9861-git-commit-template