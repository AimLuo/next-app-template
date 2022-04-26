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

## template 构建说明

- 项目 `template` 使用 `pnpm` 创建
- 上传时，忽略掉对应的 `lock` 文件
