# BROKE WORKS 与 reveal.js 上游

本作品集基于 [reveal.js](https://github.com/hakimel/reveal.js)。当前对齐官方稳定版 **6.0.2**，通过合并发布标签保留上游历史，以便后续继续合并更新。

项目内容位于 `index.html`、`images/recovered/` 和 `PBLPaper/`；根目录的 `README.md` 保留上游使用说明。首页使用仓库中的 `dist/` 构建产物，因此静态托管无需安装 Node.js。

## 本地开发与验证

构建和开发需要 Node.js 22.12 或更新版本。

```sh
npm ci
npm start
npm run build
npm test
```

`npm start` 默认使用端口 8000。修改框架源码后运行 `npm run build`，并提交生成的 `dist/` 文件，确保静态网站也获得更新。

## 后续更新

`upstream` 指向官方仓库。选择官方稳定发布标签，在新分支合并：

```sh
git fetch upstream --tags
git switch -c sync/revealjs-next
git merge <release-tag>
```

解决冲突时保留作品集正文、本地图片和报告，并根据官方升级说明迁移首页资源路径和插件注册。完成后重新构建、运行测试，并检查桌面和手机上的幻灯片、图片加载、自动播放以及打印页面。

## 本次对齐验证

- `npm run build` 通过。
- 上游 `npm test`：411/415 项通过，4 项断言失败均在 `test/test-mathjax4.html` 的公式渲染测试中。此文件及 MathJax 插件源码保持上游原样；作品集首页未加载 MathJax。
- 使用普通静态服务器在 `/BROKE-WORKS/` 子路径验证：21 张幻灯片、15 张正文图片、共用背景图、5 个插件、键盘导航、手机幻灯片模式、21 页 PDF 布局及 PBL 报告的 6 张图片均正常，未发现页面脚本错误或本地资源请求失败。
- 安装时 npm 报告 14 项依赖漏洞（5 moderate、9 high）；此次保留上游锁文件，尚未单独升级这些开发依赖。
