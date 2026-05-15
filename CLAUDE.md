# 大骐英语网站 — Claude 工作手册

> 每次打开这个项目，先完整读这个文件，再动手。

---

## 一、项目基本信息

| 项目 | 内容 |
|------|------|
| 网站名称 | 大骐英语 |
| 线上地址 | https://louisliu1205.github.io/my-website/ |
| 本地路径 | `/Users/liuruiqi/my-website/` |
| GitHub 仓库 | https://github.com/louisliu1205/my-website |
| 部署方式 | GitHub Pages，推送 main 分支后 2-3 分钟自动更新 |
| 用途 | 个人品牌展示 + PTE/雅思教学工具（互动练习页面） |

---

## 二、用户信息与偏好

### 基本信息
- **姓名**：大骐（本名刘睿琦）
- **微信**：ptedaqi
- **邮箱**：louisliu1201@gmail.com
- **GitHub 用户名**：louisliu1205
- **所在地**：中国，线上教学

### 工作偏好（重要）
- **不会写代码，不想学**，所有代码工作由 Claude 全权处理
- **沟通语言**：中文
- **不喜欢频繁确认**：能自动执行的就直接做，不要反复问"你确定吗"
- **只看结果**：改完告诉他"推送好了，2 分钟后上线"，不需要解释技术细节
- **反馈方式**：直接说哪里不对要怎么改，Claude 直接改掉，不需要讨论方案

### 教学业务
- PTE 零基础教学（从发音 ABC 开始）
- PTE 系统备考（WFD / RS / DI / SGD / RTS / SWT / WE 全题型）
- 雅思全科辅导（目标 5 分）
- 出国留学咨询

---

## 三、文件夹结构

```
my-website/
├── index.html          # 首页（品牌展示）
├── courses.html        # 课程体系页
├── wfd.html            # WFD 听写练习工具
├── styles.css          # 首页专用样式（index.html 使用）
├── wfd_data.json       # WFD 题库（唯一数据源，178 条）
├── audio/              # WFD 配套音频（177 个文件，mp3/wav/m4a）
│   ├── 23395_PTEGO.mp3
│   ├── 23380_PTEGO.mp3
│   └── ...（文件名规则：题号_PTEGO.格式）
├── CLAUDE.md           # 本文件（给 Claude 看的工作手册）
├── README.md           # 给人看的简介
└── .claude/
    └── settings.json   # Claude 权限白名单
```

---

## 四、每个文件的作用

### `index.html` — 首页
品牌落地页，面向潜在学生。结构：
1. **导航栏**：Logo（大骐英语）+ 链接（关于 / 服务 / 课程 / WFD练习 / 联系）
2. **Hero 区**：大标题 "从 ABC 开始，走到雅思五分" + 两个 CTA 按钮（加微信咨询、查看课程）
3. **关于我**：大骐的介绍，双栏布局
4. **服务列表**：4 张卡片（英语零基础教学 / PTE 系统备考 / 雅思全科辅导 / 出国留学咨询）
5. **联系方式**：微信 ptedaqi / 邮箱 / 服务范围
6. **Footer**：© 大骐英语

### `courses.html` — 课程体系页
教学内容展示，面向已报名或想了解课程的学生。结构：
- **Tab 导航**（5 个，PTE 口语为默认第一个）：
  - 🎙️ PTE 口语（RA / RS / DI / SGD / RTS）
  - 👂 PTE 听力（WFD / SST）
  - ✍️ PTE 写作（SWT / WE）
  - 🎯 考试策略
  - 🔤 零基础发音（Lesson 1-5）
- 每个题型有：题型介绍卡片 + 可展开的模板详情
- 内容来源：大骐的 59 页纸质讲义（零基础26.05班）

**注意**：courses.html 内嵌了所有样式（`<style>` 标签），不依赖 styles.css。

### `wfd.html` — WFD 听写练习
交互式练习工具，是目前最核心的功能页。功能：
- **左侧栏**：8 个话题分类过滤 + 错题复习模式
- **主区域**：音频播放 → 实时反馈输入 → 提交批改
- **实时反馈**：每打完一个词按空格立刻变色（绿=对，红=错，蓝=正在打）
- **提交后**：逐词对比（绿=写对，红删除线=漏写，黄=多写）+ 中文译文
- **统计**：答对数、答错数、正确率实时更新
- **导航**：上一题 / 下一题 / 跳过 / 显示答案
- **快捷键**：Ctrl+空格播放，Ctrl+Enter提交，Ctrl+→下一题

**数据来源**：`wfd_data.json`（加载后渲染，不刷新页面）

### `wfd_data.json` — WFD 题库
JSON 数组，每条格式：
```json
{
  "id": "23395",
  "en": "A university degree is required for entry into various professions.",
  "zh": "大学学位是进入许多行业的必要条件。",
  "audio": "23395_PTEGO.mp3",
  "category": "📚 学习课程"
}
```
- 共 178 条，177 条有配套音频
- 这是唯一数据源，wfd.html 直接 fetch 这个文件
- **修改时不要改文件格式，只增减条目**

### `styles.css` — 首页样式
只供 `index.html` 使用。courses.html 和 wfd.html 各自有内嵌 `<style>`。

---

## 五、设计规范

### 颜色系统（来自 styles.css，全站统一）
```
背景色      --bg:          #ffffff   白色
次背景      --bg-alt:      #f6f8fa   极浅灰（GitHub 风格）
主文字      --fg:          #1f2328   近黑
次文字      --fg-soft:     #59636e   中灰
弱文字      --fg-mute:     #848e98   浅灰
边框        --line:        #d1d9e0   中灰边框
浅边框      --line-soft:   #eaeef2   极浅边框
强调色      --accent:      #1f6feb   蓝色（GitHub Blue）
成功/正确   --green:       #1a7f37
错误/错误   --red:         #cf222e
警告/注意   --yellow:      #9a6700
```

### 字体
- 主字体：`"Inter"`（西文）+ `"Noto Sans SC"`（中文）
- fallback：`-apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Microsoft YaHei", sans-serif`
- 正文 16px，行高 1.6
- 标题：font-weight 700，letter-spacing -0.02em 到 -0.03em（紧缩感）

### 视觉风格
- **整体参考**：GitHub UI 风格——干净、克制、大量留白
- **圆角**：`--radius: 12px`（卡片），按钮 8px，小元素 6px
- **阴影**：极轻，只在 hover 时出现（`box-shadow: 0 6px 20px rgba(31,35,40,.07)`）
- **动效**：微妙过渡 0.15-0.2s ease，hover 时 `translateY(-2px)`
- **Nav**：sticky 吸顶，毛玻璃效果（`backdrop-filter: blur(12px)`）

### 按钮规范
```
btn--primary  背景 #1f2328（近黑），白字
btn--ghost    透明背景，近黑字，灰色边框
hover 效果    背景加深，轻微上移 translateY(-1px)
```

### 响应式
- 最大宽度：`--maxw: 1080px`（首页），720px（课程/WFD 内容区）
- 移动端断点：640-720px，双栏变单栏，cards 变单列

---

## 六、各页面模块说明

### courses.html 的 tab 切换逻辑
```javascript
// tab 顺序（DOM 顺序，对应 path-section 的 id 后缀）
const tabs = ['speaking','listening','writing','strategy','zero'];
// 对应 section id：path-speaking, path-listening, path-writing, path-strategy, path-zero
```
- 默认激活：`path-speaking`（PTE 口语）
- 折叠展开：`.lesson-hdr` 点击切换 `.lesson-body.open`
- 详情展开：`openDetail('rs')` 显示 `#detail-rs` div

### wfd.html 的数据流
```
fetch('wfd_data.json')
  → 解析 178 条
  → buildQueue()（按当前 category 过滤）
  → renderQ()（显示当前题）
  → 用户播放音频 → 输入 → input 事件实时更新 live-box → checkAnswer()
```

### WFD 8 个话题分类
| 分类 | 覆盖内容 | 题数 |
|------|----------|------|
| 🏫 校园场所 | 图书馆、礼堂、咖啡厅、地点 | 22 |
| 📚 学习课程 | 教授、作业、考试、课程 | 51 |
| 🔬 科学实验 | 化学、实验、生物 | 7 |
| 💊 健康生活 | 睡眠、健康、运动 | 7 |
| 🌍 社会文化 | 文化、社会、沟通 | 18 |
| 🌿 环境科技 | 气候、科技、环境 | 12 |
| 💼 职业商业 | 商业、职业、经济 | 12 |
| 📝 综合其他 | 以上都不是 | 49 |

---

## 七、常见操作指南

### 更新 WFD 句子
用户发来新句子（PDF / 截图 / 文字），步骤：
1. 读取 `wfd_data.json`
2. 在数组**开头**添加新条目（保持格式一致）
3. 音频文件放进 `audio/`，命名：`题号_PTEGO.mp3`
4. 推送：
   ```bash
   cd /Users/liuruiqi/my-website
   git add wfd_data.json audio/
   git commit -m "Update WFD: add X new sentences"
   git push
   ```

### 修改课程页内容
- 找到 `courses.html` 对应的 `path-section`
- 模板块用 `<div class="lesson-sec">` 包裹
- 内容块用 `<div class="tip-box">` 或 `<div class="template-box">`
- 模板占位符用 `<span class="placeholder">【xxx】</span>`

### 修改首页文案
直接 Edit `index.html`，修改对应文字内容即可。

### 推送任何改动
```bash
cd /Users/liuruiqi/my-website
git add 文件名（或 . 表示全部）
git commit -m "改了什么"
git push
```
**macOS keychain 已配好**，push 无需输入密码。

---

## 八、待完善的内容（下次继续）

- [ ] 大作文模板需要按用户实际教学内容修正（现有版本不准确）
- [ ] 口语部分有细节需要大骐本人微调（RS/DI 的一些评分说明）
- [ ] 雅思相关内容尚未添加（目前只有 PTE）
- [ ] 精华资料（314 页）内容还没整合进课程页（口语 RS/DI 每周预测题等）

---

## 九、技术栈说明

- **纯静态站**，无框架，无构建工具，直接写 HTML/CSS/JS
- **不使用** React / Vue / Node / npm 等
- 所有页面均可直接双击 `.html` 文件在浏览器打开本地预览
- wfd.html 需要从 `wfd_data.json` fetch 数据，本地预览需要起一个简单服务器：
  ```bash
  cd /Users/liuruiqi/my-website && python3 -m http.server 8000
  ```
  然后访问 http://localhost:8000/wfd.html
