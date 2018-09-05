---
title: 使用ESlint和Prettier配置React项目
date: 2018-09-05 11:56:00
tags: 前端工程
author: maiyan
---

# 使用 ESlint 和 Prettier 配置 React 项目

## 背景

### Q: ESlint 不是自带格式化吗？为什么还要用 Prettier。

    A: ESlint的重心在代码质量，Prettier只关心代码格式。

### Q: Editorconfig 又起了什么作用？

    A: EditorConfig可以帮助开发者在不同的编辑器和IDE之间定义和维护一致的代码风格。

## 介绍

### [Prettier](https://github.com/prettier/prettier) 一个简洁的代码格式化工具

### [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier) 使用 eslint 兼容 Prettier 的规则

### [lint-staged](https://github.com/okonet/lint-staged) 和 [husky](https://github.com/typicode/husky) git 的 hook 钩子工具

## 安装

### 1. 安装 `eslint` 相关

1.1 运行 `npm i -D eslint babel-eslint eslint-config-airbnb eslint-plugin-jsx-a11y eslint-plugin-react`

1.2  新建 `.eslintrc.js`

```js
module.exports = {
  parser: "babel-eslint",
  extends: ["airbnb", "prettier"]
};
```

### 2. 安装 `prettier` 相关

2.1 运行 `npm i -D prettier eslint-config-prettier`

2.2 新建 `.prettierrc`

```js
{
  "singleQuote": true,
  "trailingComma": "es5",
  "printWidth": 100,
  "overrides": [{
    "files": ".prettierrc",
    "options": {
      "parser": "json"
    }
  }]
}
```

### 3. 配置 Pre-commit Hook  git 提交前格式化和检查代码

3.1 运行 `npm i -D lint-staged husky`

### 4. 修改`package.json`

```js
{
  "scripts": {
    "lint": "eslint --ext .js src",
    "lint:fix": "eslint --fix --ext .js src",
    "lint-staged": "lint-staged",
    "lint-staged:js": "eslint --ext .js src",
    "format": "prettier --write ./src/**/**/**/*.js"
  },
   "lint-staged": {
    "**/*.js": [
      "prettier --write",
      "git add"
    ],
    "**/*.js": "npm run lint-staged:js"
  }
}
```

## 参考

[ant-design-pro](https://pro.ant.design)

[用 Prettier 格式化 JavaScript 代码](http://www.infoq.com/cn/articles/using-prettier-format-javascript-code)

[EditorConfig 的介绍](http://www.alloyteam.com/2014/12/editor-config)
