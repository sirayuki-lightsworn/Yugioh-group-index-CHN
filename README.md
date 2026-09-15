# 游戏王群索引 · 正式版（提交 + 审核 + 发布）

公开地址（设置好后仍是）：
https://sirayuki-lightsworn.github.io/Yugioh-group-index-CHN/

需要上传到仓库**根目录**的文件：

- `index.html`（本页程序）
- `data.json`（公开索引数据）
- 可选：`worker.js`（匿名提交中转）
- 可选：`.github/ISSUE_TEMPLATE/group-submit.yml`

不要只传 html。没有 `data.json` 页面是空的。

## 大家怎么用

1. 打开网页，点 **提交新群**，填群名和群号。
2. 管理员登录后打开 **审核队列**，通过时可改内容再写入索引。
3. 点 **发布到网站**，全网刷新就能看到。

## 你需要做的一次性设置

### A. 上传这两个主文件

把本目录的 `index.html` 和 `data.json` 覆盖到仓库根目录。
原来只有一个 html 的，请改成这两个文件并存。

### B. 做一枚「发布用」Token（只给你自己用）

1. GitHub 右上角头像 → Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate
2. Repository access：只选 `Yugioh-group-index-CHN`
3. Permissions：
   - Contents：Read and write
   - Issues：Read and write
4. 生成后复制 token
5. 打开索引网页 → 管理员 → **发布设置** → 粘贴 Token 并保存  
   Token 只存在你这台电脑的浏览器里，不要发给别人，也不要写进仓库。

### C. 让普通用户不用 GitHub 也能提交（推荐）

不配中转的话，用户提交会跳到 GitHub 开 Issue，没有 GitHub 账号会卡。

推荐用免费 Cloudflare Worker 接匿名提交：

1. 注册 https://dash.cloudflare.com
2. Workers & Pages → Create → Worker
3. 把 `worker.js` 全文贴进去
4. Settings → Variables：
   - `GITHUB_TOKEN`：另做一枚 **只开 Issues 写权限** 的 Fine-grained Token（不要用发布那枚）
   - `GITHUB_OWNER`：`sirayuki-lightsworn`
   - `GITHUB_REPO`：`Yugioh-group-index-CHN`
5. 部署后得到 `https://xxxx.workers.dev`
6. 在网页「发布设置」里填入 **提交中转地址**，再点一次「发布到网站」把这个地址写进 `data.json`

仓库 Issues 里建一个标签：`group-submit`（若模板已创建会自动带上）。

## 日常流程

用户提交 → 你点审核队列 → 通过并改字段 → 点「发布到网站」→ 等半分钟刷新公开页。

有未发布修改时，页头日期旁会提示。
