# 大骐英语网站 — Claude 工作说明

这个文件是给 Claude 看的。任何时候打开这个项目，先读这里。

## 项目概况

- **网站地址**: https://louisliu1205.github.io/my-website/
- **本地路径**: /Users/liuruiqi/my-website/
- **GitHub**: https://github.com/louisliu1205/my-website
- **用途**: 大骐英语的个人品牌 + PTE/雅思教学工具站

## 页面结构

| 文件 | 作用 |
|------|------|
| index.html | 首页：品牌介绍、服务、联系方式 |
| courses.html | 课程体系：零基础发音 + PTE 所有题型模板 |
| wfd.html | WFD 听写练习：178 题 + 实时反馈 + 话题筛选 |
| wfd_data.json | WFD 题库数据（唯一数据源） |
| audio/ | 177 个 WFD 配套音频文件 |

## 用户信息

- **姓名**: 大骐（本名刘睿琦）
- **微信**: ptedaqi
- **邮箱**: louisliu1201@gmail.com
- **GitHub 用户名**: louisliu1205
- **语言**: 中文（所有交流和页面内容均为中文）
- **技术水平**: 不会写代码，不想学，需要完全代劳

## 常见更新任务

### ① 更新 WFD 句子（最常见）

用户会发来新的句子，格式可能是 PDF / 截图 / 文字。步骤：

1. 读取 `/Users/liuruiqi/my-website/wfd_data.json`
2. 在 JSON 数组**头部**添加新句子，格式：
   ```json
   {
     "id": "题号",
     "en": "English sentence here.",
     "zh": "中文译文",
     "audio": "题号_PTEGO.mp3",
     "category": "📚 学习课程"
   }
   ```
3. 分类参考（根据句子内容选一个）：
   - `🏫 校园场所` — 图书馆、礼堂、咖啡厅、校园地点
   - `📚 学习课程` — 教授、作业、考试、课程、学位
   - `🔬 科学实验` — 化学、实验、生物
   - `💊 健康生活` — 睡眠、健康、运动
   - `🌍 社会文化` — 文化、社会、沟通
   - `🌿 环境科技` — 气候、科技、环境
   - `💼 职业商业` — 商业、职业、经济
   - `📝 综合其他` — 以上都不是
4. 如果用户同时提供了音频 zip，解压到 audio/ 目录
5. 提交 + 推送：
   ```bash
   cd /Users/liuruiqi/my-website
   git add wfd_data.json audio/
   git commit -m "Update WFD: add N new sentences"
   git push
   ```

### ② 修改网页文字

直接 Edit 对应 html 文件，然后 git add + commit + push。

### ③ 添加新课程内容

在 courses.html 里找对应的 path-section，按已有格式添加 lesson-sec 块。

### ④ 添加新音频

把音频文件放进 audio/ 目录，命名规则：`题号_PTEGO.mp3`（或 .wav/.m4a）。
然后在 wfd_data.json 里对应条目的 "audio" 字段填上文件名。

## Git 推送方法

```bash
cd /Users/liuruiqi/my-website
git add 文件名
git commit -m "描述改了什么"
git push
```

用户已配好 macOS keychain，push 会自动用已保存的 token，不需要再输入密码。

## 注意事项

- 用户不看代码，只看效果，所有改动要用预览面板确认
- 推送后 2-3 分钟 GitHub Pages 自动更新
- wfd_data.json 是 WFD 功能的唯一数据源，不要分裂成多个文件
