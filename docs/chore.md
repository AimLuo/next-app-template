# 记录

- 使用 [.gitignore Generator](https://marketplace.visualstudio.com/items?itemName=piotrpalarz.vscode-gitignore-generator) 生成 `.gitignore`

  > 使用 [.gitignore Generator](https://marketplace.visualstudio.com/items?itemName=piotrpalarz.vscode-gitignore-generator) 时，可能需要挂代理，因为它会访问 [gitignore.io API](https://gitignore.io/)

  - webstorm
  - visualstudiocod
  - node
  - macos

- 增加忽略 `lock` 文件

  ```ini
  ### this project required ###
  # Lock
  pnpm-lock.yaml
  yarn.lock
  package-lock.json
  ```

- 项目使用 `pnpm` 管理

## base 构建说明

### 初始化

```shell
pnpm create next-app -- --ts
```

打开 `base` 目录，删除 `.git` 版本控制

### 添加额外的 eslint 配置

```shell
pnpm add -D @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-plugin-simple-import-sort
```

修改 `.eslintrc.json`

```shell
{
  "plugins": ["simple-import-sort"],
  "extends": ["next/core-web-vitals", "plugin:@typescript-eslint/recommended"],
  "rules": {
    "@typescript-eslint/no-unused-vars": "error",
    "@typescript-eslint/no-explicit-any": "error",
    "simple-import-sort/imports": "warn",
    "simple-import-sort/exports": "warn"
  }
}

```

修改 `lint` 命令

```json
"lint": "eslint ./ --ext js,jsx,ts,tsx --fix"
```

针对 `vs code` 安装 [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) 扩展，启用自动修复，打开 `vs code` 设置中的 `Code Actions On Save` 增加

```json
  "editor.codeActionsOnSave": {
    "source.fixAll": true
  },
```

> `source.fixAll` 表示启用了所有扩展程序的修复功能，你也可以只启用 ` "source.fixAll.eslint": true`

### 添加 `prettier`

```shell
pnpm add -D prettier eslint-config-prettier
```

增加 `.prettierrc.json`

```json
{
  "semi": false,
  "trailingComma": "es5",
  "singleQuote": true,
  "tabWidth": 2,
  "jsxSingleQuote": true,
  "useTabs": false
}
```

修改 `.eslintrc.json`

```json
{
  "plugins": ["@typescript-eslint", "simple-import-sort"],
  "extends": [
    "next/core-web-vitals",
    "plugin:@typescript-eslint/recommended",
    "prettier"
  ],
  "rules": {
    "@typescript-eslint/no-unused-vars": "error",
    "@typescript-eslint/no-explicit-any": "error",
    "simple-import-sort/imports": "warn",
    "simple-import-sort/exports": "warn"
  }
}
```

针对 `vs code` 安装 [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) 扩展，打开 `vs code` 设置：

- `Default Dormatter` 改为 `prettier`
- 启用 `Format On Save`

### 增加 import baseUrl

`tsconfig.json` 中添加

```json
"baseUrl": "."
```

就可以这样用了

```ts
import "styles/globals.css";
import styles from "styles/Home.module.css";
```

### 增加 svg 组件

安装

```shell
pnpm add -D @svgr/webpack
```

修改 `next.config.js` 配置

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  webpack(config) {
    config.module.rules.push({
      test: /\.svg$/i,
      issuer: /\.[jt]sx?$/,
      use: ["@svgr/webpack"],
    });
    return config;
  },
};

module.exports = nextConfig;
```

就可以这样用了

```ts
import Foo from "icons/foo.svg";
const Test = () => (
  <div>
    test <Foo />
  </div>
);
```

## tailwindcss 构建

基于 `base` 创建

### 增加 tailwindcss 依赖

参考 [next typesctipt](https://nextjs.org/docs/basic-features/typescript) 与 [Install Tailwind CSS with Next.js](https://tailwindcss.com/docs/installation/framework-guides)
其中的命令改为用 `pnpm` 执行

```shell
pnpm add -D tailwindcss postcss autoprefixer
pnpx tailwindcss init -p
```

针对 `vs code` 参考 [Editor Setup](https://tailwindcss.com/docs/editor-setup) 安装 `PostCSS Language Support` 和 `Tailwind CSS IntelliSense`
