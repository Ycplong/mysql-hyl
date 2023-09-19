## githooks

| git hook              | 执行时机                                                     | 说明                                                         |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| applypatch-msg        | git am 执行前                                                | 默认情况下，如果commit-msg启用的话，applpatch-msg钩子在启用时会运行commit-msg钩子 |
| pre-applypatc         | git am 执行前                                                | 默认的pre-applypatch钩子在启用时运行pre-commit钩子（如果后者已启用） |
| post-applypatch       | git am 执行后                                                | 这个钩子主要用于通知，不能影响git-am的结果                   |
| pre-commit            | git commit 执行前                                            | 可以使用 git commit --no verify 命令绕过该钩子               |
|                       |                                                              |                                                              |
| re-merge-commit       | git merge 执行前                                             | 可以使用 git merge --no verify 命令绕过该钩子                |
| prepare-commit-msg    | git commit执行之后，编辑器打开之前                           |                                                              |
|                       |                                                              |                                                              |
| ommit-msg             | git commit 执行前                                            | 可以使用 git commit --no verify 命令绕过该钩子               |
| post-commit           | git commit 执行后                                            | 不影响git commit的结果                                       |
| pre-rebase            | git rebase执行前                                             |                                                              |
| ost-checkout          | git checkout 或 git switch执行后                             | 如果不使用 --no-checkout 参数，则在 git clone 之后也会执行   |
| post-merge            | git merge 执行后                                             | 在执行git pull 时也会被调用                                  |
| pre-push              |                                                              | git push 执行前                                              |
| pre-receive           | git receive pack 执行前                                      |                                                              |
| update                |                                                              |                                                              |
| proc-receive          |                                                              |                                                              |
| post-receive          | git receive pack 执行前                                      | 不影响 git receive pack 的执行结果                           |
| post-update           | 当git receive pack对 git push 作出反应并更新仓库中的引用时   |                                                              |
| reference-transaction |                                                              |                                                              |
| push-to-checkout      | 当git receive pack对 git push 作出反应并更新仓库中的引用时，以及当推送试图更新当前被签出的分支且 receive.denyCurrentBranch配置被updateInstead时 |                                                              |
| pre-auto-gc           | git gc --auto 执行前                                         |                                                              |
| post-rewrite          | 执行 git commit --amend 或 git rebase 时                     |                                                              |
| sendemail-validate    | git send-email 执行前                                        |                                                              |
| fsmonitor-watchman    | 配置core.fsmonitor被设置为.git/hooks/fsmonitor-watchman 或.git/hooks/fsmonitor-watchmanv2时 |                                                              |
| p4-changelist         | git-p4 submit 执行并编辑完changelist message 之后            | 可以使用 git-p4 submit --no-verify绕过该钩子                 |
| 4-prepare-changelist  | git-p4 submit 执行后，编辑器启动前                           | 可以使用 git-p4 submit --no-verify绕过该钩子                 |
| p4-post-changelist    | git-p4 submit 执行后                                         |                                                              |
| p4-pre-submit         | git-p4 submit 执行前                                         | 可以使用 git-p4 submit --no-verify绕过该钩子                 |
| post-index-change     | 索引被写入 read-cache.c do_write_locked_index后              |                                                              |



## git commit提交规范

~~~javascript
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
~~~

- `<type>`代表某次提交的类型，比如是修复一个 bug 或是增加一个 feature，具体类型如下：

| 类型     | 描述                                                   |
| -------- | ------------------------------------------------------ |
| feat     | 新增feature                                            |
| fix      | 修复bug                                                |
| docs     | 仅仅修改了文档，比如README, CHANGELOG, CONTRIBUTE等等; |
| style    | 仅仅修改了空格、格式缩进、逗号等等，不改变代码逻辑;    |
| refactor | 代码重构，没有加新功能或者修复bug                      |
| perf     | 优化相关，比如提升性能、体验                           |
| test     | 测试用例，包括单元测试、集成测试等                     |
| chore    | 改变构建流程、或者增加依赖库、工具等                   |
| revert   | 回滚到上一个版本                                       |

- `scope`：说明commit影响的范围。scope依据项目而定，例如在业务项目中可以依据菜单或者功能模块划分，如果是组件库开发，则可以依据组件划分。
- `subject`:是commit的简短描述；
- `body`:提交代码的详细描述；
- `footer`:如果代码的提交是不兼容变更或关闭缺陷，则footer必需，否则可以省略。

 ### Husky

[Husky](https://link.juejin.cn/?target=https%3A%2F%2Ftypicode.github.io%2Fhusky):在做前端工程化时`husky`可以说是一个必不可少的工具。`husky`**对 git 的 commit 操作进行校验**,`husky`继承了Git下所有的钩子，在触发钩子的时候。 配合`lint-staged`在提交代码之前运行 Linting更有意义。通过这样做，您可以确保没有错误进入存储库并强制执行代码样式。`husky`可以阻止不合法的commit，push等等

#### 使用husky

- 首先执行安装命令  `npm install husky --save-dev`
- 要在安装后自动启用钩子，我们需要执行`npm set-script prepare "husky install"`
- 执行完上一步的命令之后可以在package.json 文件的scripts配置项中看到如下代码：

```js
"scripts": {
    "prepare": "husky install"
}
复制代码
```

- 创建钩子，比如我们创建一个commit-msg钩子：`yarn husky add .husky/commit-msg 'yarn commitlint --edit "$1"'`
- 将上一步创建的 commit-msg 钩子添加到git中：`git add .husky/commit-msg`
- 此外还有 `husky-init`命令， 执行之后可以在项目中快速的初始化一个husky。

### lint-staged

我们配置好了`husky`后，会出现一个问题，就是我们不管是改动一行还是两行都会对整个项目进行[代码检查](https://cloud.tencent.com/product/tcap?from=10680)和格式化，我们可以通过`lint-staged`这个工具来实现只对`git`**暂存区**中的内容进行检查和格式化，配置步骤如下：

1、**安装lint-staged**

~~~javascript
npm run lint-staged --dev
~~~

2、**配置package.json**

~~~javascript
{
  "scripts": {},
  // 新增
  "lint-staged": {
    "*.{vue,js,ts,tsx,jsx}": [
      "eslint --fix",
      "prettier --write --ignore-unknown"
    ]
  },
}
~~~

3、**修改.husky/pre-commit，修改内容如下：**

~~~javascript
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

npx lint-staged
~~~

~~~javascript
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx lint-staged --allow-empty $1 
~~~

- **--allow-empty**：使用此参数允许创建空的git提交。默认情况下，当LITER任务撤消所有阶段性的更改时，LITET阶段将抛出一个错误，并中止提交。

## git hooks规范实现

- 首先我们来安装需要用到的依赖，执行以下命令：
- 执行 `yarn add husky -D` 安装husky。
- 接着执行 `npm set-script prepare "husky install"` 之后，可以在package.json文件的scripts配置项中看到 `"prepare": "husky install"`

**ps:** 执行`yarn set-script prepare "husky install"` 会报错：`error Command "set-script" not found.`

- 继续执行 `yarn prepare`之后，可以在项目的根目录下看到多了如下图所示的目录：

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6e452c75dcd4453d9f09d48ce4528c61~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

- 如果执行`yarn prepare`之后报如下图所示错误，则需要执行`git init`然后再执行`yarn prepare`

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cd27bbdf20094e5db1210059e737b9db~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

- husky 准备好之后，我们接着来安装其他的用于规范，检查代码的依赖。
- 执行`yarn add lint-staged -D`
- 执行`yarn add eslint prettier -D`
- 在package.json文件下添加如下代码：

~~~javascript
"lint-staged": {
    "src/**/*.{js,jsx,ts,tsx,json}": [
      "prettier --write",
      "eslint",
      "git add"
    ]
}
~~~

~~~javascript
  "lint-staged": {
    "**/*.{vue,js,jsx,ts,tsx,cjs,json,css,scss}": [
      "prettier --cache --write",
      "git add"
    ],
    "**/*.{vue,js,jsx,ts,tsx}": [
      "eslint --cache --fix",
      "git add"
    ],
    "**/*.{css,less,scss,vue,html}": [
      "stylelint --cache --fix",
      "git add"
    ]
  },
// 注意：stylelint报错  如果改动的样式文件都被忽略了，那么就会出现 【Error: All input files were ignored because of the ignore pattern. Either change your input, ignore pattern or use "--allow-empty-input" to allow no inputs】的报错， 解决思路修改package.json的配置 "stylelint --fix --allow-empty-input"
~~~

- 开始配置eslint约束相关的东西：执行 `npx eslint --init` 然后按照提示一步步操作即可。[具体配置步骤查看](https://link.juejin.cn?target=https%3A%2F%2Fblog.csdn.net%2Fm0_64564920%2Farticle%2Fdetails%2F123998369)
- 执行`yarn add @commitlint/cli @commitlint/config-conventional -D`安装commitlint相关依赖，用来帮助我们在多人开发时，遵守 git 提交约定。
- 执行`echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js`在根目录创建 commitlint.config.js 文件（当然也可以手动创建此文件），其内容如下所示：

```js
module.exports = {
  extends: [
    "@commitlint/config-conventional"
  ],
  // 以下时我们自定义的规则
  rules: {
    'type-enum': [
      2,
      'always',
      [
        'bug', // 此项特别针对bug号，用于向测试反馈bug列表的bug修改情况
        'feat', // 新功能（feature）
        'fix', // 修补bug
        'docs', // 文档（documentation）
        'style', // 格式（不影响代码运行的变动）
        'refactor', // 重构（即不是新增功能，也不是修改bug的代码变动）
        'test', // 增加测试
        'chore', // 构建过程或辅助工具的变动
        'revert', // feat(pencil): add ‘graphiteWidth’ option (撤销之前的commit)
        'merge' // 合并分支， 例如： merge（前端页面）： feature-xxxx修改线程地址
      ]
    ]
  }
};

复制代码
```

- 如果还需要别的代码优化依赖包，可以接着进行安装
- 至此，准备好我们需要的依赖包之后，我们开始添加钩子
- 执行`yarn husky add .husky/commit-msg 'yarn commitlint --edit "$1"'`之后，会看到在根目录的`.husky`文件夹下多了一个 `commit-msg` 文件，其内容如下：

```js
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

yarn commitlint --edit "$1"
```

~~~javascript
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

echo "========== 执行 commit-message 校验 =========="

echo "========== message 的格式“必须”为 type: subject/description =========="

echo "========== 注意：英文冒号、英文空格 =========="

echo "========== type “必须”是这几种：feat, fix, bug, style, refactor, perf, docs, test, build, ci, revert, merge, chore =========="

npx commitlint --edit $1
~~~



- 紧接着，我们需要将上一步添加的钩子添加到git中去，执行`git add .husky/commit-msg`
- 执行`yarn husky add .husky/pre-commit 'yarn lint-staged --allow-empty "$1"'`之后，会看到在根目录的`.husky`文件夹下多了一个 `pre-commit` 文件，其内容如下：

```js
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

yarn lint-staged --allow-empty "$1"
```

- 同样的，我们需要将上一步添加的钩子添加到git中去，执行`git add .husky/pre-commit`
- 接下来，就是检验我么配置的时候了：当我们按照 commit规范正确提交时，可以在控制台看到如下输出

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2f95bad7174b422cab42b6ef64686bbd~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

- 当我们不按照配置的规范来提交commit时，就会发现如下报错，并阻止你提交代码

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ea5260a7b47c4d32b9aa1d526d64b397~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

- 至此，我们的钩子配置已经完美收官！

