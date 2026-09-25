# TinyAudio — 论文项目页

纯静态 HTML，无构建步骤，推 `main` 即自动发布到 https://tinyaudio-project.github.io/

复刻自 Resonate（https://resonatedemo.github.io）与 MeanAudio（https://MeanAudio.github.io）的 demo page，
两者都基于 [Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template)
（Nerfies 派生，Bulma 内核）。本页用了同一套模板、同一批静态资源、同样的 section 顺序。

## 页面结构

1. `hero` — 标题 / 作者与单位 / Paper·arXiv·Code·Audio samples 链接
2. `hero teaser` — 论文 Fig. 1（AudioCaps 质量 vs 生成器参数量气泡图）+ 概述段落
3. `section hero is-light` — **Audio Generation Samples**（音频对比表）
4. `hero teaser` — **Overall Architecture**（论文 Fig. 2，单流 TA-DiT）
5. `hero teaser` — **Main Results**（Table 1 全量）
6. `footer` — 模板出处

## 结构

```
index.html          # 唯一页面，样式内联在 <style> 里
.nojekyll           # 必须保留：否则 Jekyll 会吞掉下划线开头的文件
static/
  css/  js/         # 模板自带资源（bulma / fontawesome），本地引用
  images/           # fig1_teaser.png、fig2_architecture.png、og.png
  audio/            # 音频样本，见 static/audio/README.md
```

## 素材来源

| 文件 | 来源 |
| --- | --- |
| `static/images/fig1_teaser.png` | `Tinyaudio_icassp2027 (4).pdf` 第 1 页内嵌位图（2929×1281） |
| `static/images/fig2_architecture.png` | 同 PDF 第 2 页内嵌位图（5888×2980） |
| `static/images/og.png` | 白底 1200×630 + Fig. 1 居中合成 |
| Table 1 | 按 PDF 文本重排为 HTML 表格，加粗/下划线沿用论文的 best / second-best 规则 |
| 音频 | 见下 |

## 加音频的规范

**不要把大体积音频直接提交进仓库。** GitHub Pages 不支持 Git LFS，单文件上限 100 MB。

页面里每个单元格的 `<audio src>` 现在写的是 `.wav`，文件名用 `NN`（`01`、`02`…），
放进 `static/audio/<系统>/` 即可，**不需要改任何代码**。
若想改用体积更小的 mp3：

```bash
ffmpeg -i in.wav -ac 1 -b:a 80k static/audio/<系统>/01.mp3
```

但要同步把 `index.html` 里对应的 `src` 后缀改成 `.mp3`（或让我把占位探测逻辑改成多后缀尝试）。

样本量大（100 条以上）时，音频改放 HuggingFace datasets 或 GitHub Releases，
页面里只留外链，避免仓库体积膨胀。

## 占位机制

`static/audio/<系统>/NN.wav` 不存在时，JS 会把该单元格的播放器换成虚线文件名占位块；
把文件放进去刷新即可自动变回可播放状态。判定用 `HEAD` 请求 + `error` 事件双保险。

`static/audio/README.md` 里有完整的文件名对照表。

## 待补

- `Paper` 与 `arXiv` 链接目前是 `#`（投稿中，尚未上线 arXiv）。
- 音频 50 个文件。
- prompt 文案目前是占位（按 TTA-Bench 的多事件/时序风格写的），需替换为实际评测用的 prompt。

## 本地预览

```bash
python3 -m http.server 8000
# 浏览器打开 http://localhost:8000/
```
