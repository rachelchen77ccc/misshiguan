# 觅食官 · Claude Code 工作规范

## 项目结构
- misshiguan.html — 主文件，所有改动在这里
- index.html — 部署用，每次改完执行 cp misshiguan.html index.html
- design-tokens.html — 不要动

## 必须遵守
- 单文件原则：不拆分，不新建 JS/CSS 文件
- 风格：暖土色系，Playfair Display + DM Sans
- sessionId 每个对话独立，发送时必须带上
- 餐厅解析靠 🍽️ 分割，改格式要同步改 parseRestaurants()
- 开始修改前，先阅读 misshiguan.html 现有结构，优先复用已有函数，不要无必要重构
- 新功能优先以增量方式实现；除非必要，不要改已有命名、DOM 结构和发送链路

## Webhook
POST https://rayrayonthemove.app.n8n.cloud/webhook/86b2b344-ceaa-4601-92b8-2dc810150356/chat  
Body: `{ action: "sendMessage", sessionId: "sid_xxx", chatInput: "..." }`  
Return: `{ output: "..." }`

## 工作方式
- 每次开始任务前，先阅读 CLAUDE.md，再阅读 misshiguan.html 相关实现
- 优先复用现有 sendMessage()、suggest()、addBot()、parseRestaurants() 等已有逻辑
- 不要重写主搜索逻辑；n8n 是黑箱
- 不要因为做新功能而破坏已有功能：多 session、欢迎页、错误处理、发送冷却、餐厅卡片渲染
- 如果要新增状态或辅助函数，尽量最小化实现，并与当前 session 机制兼容
- 除非明确要求，不要调整整体视觉风格、颜色变量、排版节奏

## 每次改完执行
cp misshiguan.html index.html && git add . && git commit -m "feat: xxx" && git push