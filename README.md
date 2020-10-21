
# Project configuration for commit message automation  

[![Join the chat at https://gitter.im/automate-commit-configuration/community](https://badges.gitter.im/automate-commit-configuration/community.svg)](https://gitter.im/automate-commit-configuration/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Commit Message Automation organize and normalize commit messages that are made in the git repository.  

This configuration use:
 - **commitizen** -> commit conventions CLI ( https://github.com/commitizen/cz-cli )  
 - **commitLint** -> a commit messages checker ( https://commitlint.js.org/ )  
 - **husky** -> a git hook/package.json bridge ( https://github.com/typicode/husky )

## How should I configure?  
  
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
  
##### 3.1 - Run commitizen configuration in your project  
`commitizen init cz-conventional-changelog --save-dev --save-exact`  
  
##### 3.2 - Add commitizen configuration for husky in package.json  
```javascript  
{  
...  
 "husky": { 
	 "hooks": { 
		 "commit-msg": "commitlint -E HUSKY_GIT_PARAMS", "prepare-commit-msg": "/dev/tty && git cz --hook || true" 
	} 
 },
 ...  
}  
```  

## How should I use?
When run 'git commit' on command line (for IDE users, check IDE plugins section), the commitizen cli runs an assistant to commit message construction.

![commitizen commits assistant](/md-images/commitizen-add-commit.png)

(example of commitizen cli)

## How a bad commit message validation looks like?
With above configuration, Husky fired pre-commit action, checking commit message with conventional commitlint format. 
This is an example of bad commit message and the checking's result.

![rejected commits examples](/md-images/error-automate-commit.png)

(example of commitLint validation error)

## IDE plugins  
Microsoft Visual Studio Code  
https://marketplace.visualstudio.com/items?itemName=KnisterPeter.vscode-commitizen  
  
JetBrains WebStorm  
https://plugins.jetbrains.com/plugin/9861-git-commit-template
