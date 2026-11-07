# 家庭摄像头 · 固定入口

`https://bietou123.github.io/cam/` 是家庭摄像头的**固定入口**。

摄像头本身跑在家庭内网，由 NAS 上的 cloudflared quick tunnel 暴露到公网；quick tunnel 每次重启都会换地址，所以这里只放一个跳转页，由 NAS 定时脚本自动更新：

- 脚本：`update_redirect.py`（仅标准库）
- 逻辑：`docker logs cam-tunnel` 里取最新的 `*.trycloudflare.com` 地址 → 与上次对比 → 变了就重渲染 `index.html` 并推送
- 跳转目标不在本仓库里，本仓库只有这个跳转页和说明

## 页面状态

- **正在跳转**：说明隧道地址有效
- **固定入口已就绪，但后台隧道还没上报地址**：NAS 上的脚本还没跑过，或容器刚重启还没拿到新地址

## 安全

- 跳转页不含任何账号、密码或凭据
- 摄像头自己的访问认证在摄像头/反向代理一端，与本页无关

## 许可

MIT
