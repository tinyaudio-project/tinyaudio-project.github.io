# tinyaudio-project.github.io

TinyAudio 论文项目页。纯静态 HTML，无构建步骤，推 `main` 即自动发布到
https://tinyaudio-project.github.io/

## 结构

```
index.html          # 唯一页面，样式内联在 <style> 里
.nojekyll           # 必须保留：否则 Jekyll 会吞掉下划线开头的文件
assets/
  audio/            # 放 mp3 / opus 音频样本
  img/              # 放 teaser.png、方法图、og.png
```

## 待替换的占位内容

都在 `index.html` 里，搜 `goes here` / `placeholder` / `not added yet` 即可定位：

- `<h1>` 论文标题与副标题
- `.authors` / `.affil` 作者与单位（作者名做成超链接指向个人主页）
- `.links` 的 Paper / arXiv / Code 链接，把 `href="#"` 换成真实地址
- `<meta name="citation_*">` 与 `og:*`，影响 Google Scholar 抓取和分享预览
- Abstract 段落、Figure 1、Citation 的 BibTeX

## 加音频的规范

**不要把 wav 提交进仓库。** GitHub Pages 不支持 Git LFS，单文件上限 100MB。

```bash
ffmpeg -i in.wav -ac 1 -b:a 80k assets/audio/01.mp3
```

页面里用这个结构替换掉对应的 `.slot` 占位块：

```html
<div class="slot">
  <b>01 &middot; 提示文本</b>
  <audio controls preload="none" src="assets/audio/01.mp3"></audio>
</div>
```

`preload="none"` 别去掉——音频多了以后它会决定页面能不能立刻打开。

样本量大（100 条以上）时，音频改放 HuggingFace datasets 或 GitHub Releases，
页面里只留外链，避免仓库体积膨胀。

## 本地预览

```bash
python3 -m http.server 8000
```

然后打开 http://localhost:8000/
