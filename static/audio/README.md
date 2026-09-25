# 音频文件清单

表格每行对应一个 prompt，5 个系统各一个文件。把对应的音频放进来，页面上的虚线占位块会自动变成播放器（无需改代码）。

命名规则：`static/audio/<系统目录>/<两位编号>.wav`

| prompt 编号 | TinyAudio | TinyAudio-MF | MeanAudio-L-Full | TangoFlux | GT |
| --- | --- | --- | --- | --- | --- |
| 01 | TinyAudio/01.wav | TinyAudio-MF/01.wav | MeanAudio-L-Full/01.wav | TangoFlux/01.wav | GT/01.wav |
| 02 | TinyAudio/02.wav | TinyAudio-MF/02.wav | MeanAudio-L-Full/02.wav | TangoFlux/02.wav | GT/02.wav |
| 03 | TinyAudio/03.wav | TinyAudio-MF/03.wav | MeanAudio-L-Full/03.wav | TangoFlux/03.wav | GT/03.wav |
| 04 | TinyAudio/04.wav | TinyAudio-MF/04.wav | MeanAudio-L-Full/04.wav | TangoFlux/04.wav | GT/04.wav |
| 05 | TinyAudio/05.wav | TinyAudio-MF/05.wav | MeanAudio-L-Full/05.wav | TangoFlux/05.wav | GT/05.wav |
| 06 | TinyAudio/06.wav | TinyAudio-MF/06.wav | MeanAudio-L-Full/06.wav | TangoFlux/06.wav | GT/06.wav |
| 07 | TinyAudio/07.wav | TinyAudio-MF/07.wav | MeanAudio-L-Full/07.wav | TangoFlux/07.wav | GT/07.wav |
| 08 | TinyAudio/08.wav | TinyAudio-MF/08.wav | MeanAudio-L-Full/08.wav | TangoFlux/08.wav | GT/08.wav |
| 09 | TinyAudio/09.wav | TinyAudio-MF/09.wav | MeanAudio-L-Full/09.wav | TangoFlux/09.wav | GT/09.wav |
| 10 | TinyAudio/10.wav | TinyAudio-MF/10.wav | MeanAudio-L-Full/10.wav | TangoFlux/10.wav | GT/10.wav |

合计 50 个文件。

## 注意

- **扩展名改了要同步改 HTML**：`<audio src>` 里写死了 `.wav`。如果想用 `.flac` / `.mp3`，把 `index.html` 里的 `static/audio/.../NN.wav` 批量替换即可。
- **页面仓库不要放 wav**：mono 单声道转成 64–96 kbps 的 mp3，或直接上 HuggingFace 放外链 + `<audio preload="none">`。GitHub Pages 单文件上限 100 MB，仓库/站点建议 ≤1 GB。
- 想换 prompt 文案，直接改 `index.html` 里每行第一个 `<td>`。
