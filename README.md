# my-website

刘睿琦的个人品牌展示站点。纯静态，无需构建工具。

## 本地预览
直接用浏览器打开 `index.html` 即可，或者在项目目录里跑：

```bash
python3 -m http.server 8000
```

然后访问 http://localhost:8000

## 修改内容
所有文字都在 [index.html](index.html) 里，直接编辑即可。样式在 [styles.css](styles.css)。

## 部署到 GitHub Pages
1. 仓库 → Settings → Pages
2. Source 选 `Deploy from a branch`，分支选 `main`，目录选 `/ (root)`
3. 保存后几分钟即可访问 `https://<你的用户名>.github.io/my-website/`
