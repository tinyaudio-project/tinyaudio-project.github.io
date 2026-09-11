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

## 内容状态

已按 `Tinyaudio_icassp2027.pdf` 填好：标题、作者与三级单位、Abstract、At a glance、
Fig. 1 / Fig. 2、Method 全文（TA-VAE / TA-CLAP / TA-DiT / SFT / MeanFlow / 训练设置）、
结果三张表（footprint 与效率、AudioCaps、TTA-Bench）、主观评测表、Ablation 表、BibTeX。

**还差的只有两处**，都标在页面上：

- `.links` 里的 `Paper (soon)` —— 等 arXiv 上线后换成真实链接，同时把
  `<meta name="citation_pdf_url">` 和 `og:url` 一并改掉
- `#samples` 段的音频样本块

另外作者名目前都是 `href="#"`，等有了主页地址再补。

## 配图来源

`assets/img/teaser.png`（Fig. 1，2929×1281）和 `assets/img/method.png`（Fig. 2，1452×725）
直接从论文 PDF 里抠的，不是重画的：

```bash
python -c "
from pypdf import PdfReader
r = PdfReader('paper.pdf')
for i, p in enumerate(r.pages, 1):
    for j, im in enumerate(p.images):
        open(f'p{i}_{j}.png', 'wb').write(im.data)
"
```

`og.png` 是 1200×630 的分享预览卡，用 Pillow 照着标题和作者行生成的，改标题后要重跑一次。


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
