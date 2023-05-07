# Vue 3 + TypeScript + Vite

This template should help get you started developing with Vue 3 and TypeScript in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Type Support For `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin) to make the TypeScript language service aware of `.vue` types.

If the standalone TypeScript plugin doesn't feel fast enough to you, Volar has also implemented a [Take Over Mode](https://github.com/johnsoncodehk/volar/discussions/471#discussioncomment-1361669) that is more performant. You can enable it by the following steps:

1. Disable the built-in TypeScript Extension
   1. Run `Extensions: Show Built-in Extensions` from VSCode's command palette
   2. Find `TypeScript and JavaScript Language Features`, right click and select `Disable (Workspace)`
2. Reload the VSCode window by running `Developer: Reload Window` from the command palette.

# git subtree 命令
## 添加子项目：
```
git subtree add --prefix=<存放子项目的相对路径> <子项目git地址> <分支> --squash
```
例如：
```
git subtree add --prefix=src/subtree https://github.com/xxx/xxx.git master
```
## 修改子项目代码
在原项目中直接commit就行，无需其他特殊配置，建议子项目代码单独commit，不要跟外围代码一起提交
## 推送子项目代码 push
命令：
```
git subtree push --prefix=<存放子项目的相对路径> <子项目git地址> <分支> --squash
```

例如：
```
git subtree push --prefix=src/subtree https://github.com/xxx/xxx.git master
```

## 拉取子项目最新代码 pull
命令：
```
git subtree pull --prefix=<存放子项目的相对路径> <子项目git地址> <分支> --squash
```

例如：
```
git subtree pull --prefix=src/subtree https://github.com/xxx/xxx.git master
```

## 其他 git subtree split
命令：
```
git subtree split --prefix=<存放子项目的相对路径> --rejoin
```

例如：
```
git subtree split --prefix=src/subtree --rejoin
```