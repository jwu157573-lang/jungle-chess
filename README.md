# 斗兽棋 · 人机对战

单文件网页游戏，零依赖，双击即玩。

- `jungle.html` —— 源文件（也是可玩的完整版本）
- `dist/index.html` —— 对外发布用的副本（静态服务器根目录）

## 玩法
红方（你）先手，黑方是电脑。点自己的棋子看可走位置，再点目标格落子。
难度：简单（贪心 + 随机）/ 普通（3 层搜索）/ 困难（迭代加深到 7 层，限时 1.2s）。

## 本地打开
直接双击 `jungle.html`。

## 重新起一个公网链接
需要一个本地静态服务器 + 一条隧道（cloudflared 已下载在 `tools/`）：

```bash
# 1) 静态服务器
node -e "require('http').createServer((q,s)=>{require('fs').readFile('dist/index.html',(e,d)=>{s.writeHead(200,{'Content-Type':'text/html; charset=utf-8'});s.end(d)})}).listen(8123,'127.0.0.1')"

# 2) 另开一个终端：临时公网地址（形如 https://xxx.trycloudflare.com）
./tools/cloudflared.exe tunnel --url http://127.0.0.1:8123
```

隧道地址随进程存活，进程关掉链接即失效。

## 永久发布
需要你自己的托管账号，任选其一：
- GitHub Pages：仓库 + Pages，一次配置长期有效
- Cloudflare Pages / Vercel / Netlify：拖拽上传 `dist/` 即可
