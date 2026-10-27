# Inland earthquake simulator (inland_quake) and window app — companion source for the book

Design documents and code for the inland earthquake simulator built in ***Toward a Million Lines XI — Building an Inland Earthquake Simulator*** (Japanese title 『LLM で 100 万行のソフトウェア開発 XI — 内陸地震のシミュレータをつくる』; the book is in Japanese).

`inland_quake` (Python) computes, **without being told where a fault is**, how faults are born and how earthquakes repeat in the crust of an inland region. The crust is a two-dimensional section (plane strain) filled with disk-shaped particles joined by bonds (a discrete-element model); the two ends are pushed or pulled at a constant speed; a bond breaks when its stress exceeds its strength, the broken face slips with friction and viscosity, and the calculation switches between a quasi-static mode (years per step) and a dynamic mode (milliseconds per step) at each earthquake. A face that slipped recovers only part of its strength quickly and the rest slowly (the recovery fraction). It runs two kinds of calculation — `folding` (a sedimentary layer on a basement is shortened and faults grow) and `longest_rupture` (a crust at lithostatic pressure is pushed or pulled, and the earthquake with the longest connected rupture is kept frame by frame) — and writes cross-section figures, an event catalogue, slip-by-depth figures, a summary table and animations. A Windows **window app** (Flutter) sets the parameters, starts the computation, shows progress and plays the animations. **The window holds no computation of its own**: every button runs an `inland_quake` command and reads the result files it writes. In this project **the design documents are the source of the code**.

## Download

**The ready-to-run app and the source are on the [Releases](../../releases) page**, not in this repository. The release has four separate ZIPs:

| File | Contents |
|:---|:---|
| `inland_quake_exe.zip` | The Windows window app, ready built (**Japanese screens**), with the simulator it runs and a small-example launcher |
| `inland_quake_exe_en.zip` | The same app (**English screens** by default), with the English-display simulator (figure and animation labels in English) |
| `inland_quake.zip` | Design documents (`docs/`, Japanese, L1-L4, the source; `docs_en/`, the complete set for English readers: L1-L3 translated into English, L4 the Japanese originals as is) in separate folders, the code (`src/inland_quake/`, its English-display variant `src_en/inland_quake/`, and `app/`), the requirements specification (131 requirements), and empty databases (`ledger/`) |
| `inland_quake_animations.zip` | The animations of the calculations of the book (a crust pushed and a crust pulled, with three values of the recovery fraction each): 18 MP4 video files |

The app needs Python 3.11 and numpy, numba, matplotlib and pillow on your PC (see the README inside the ZIPs); extract to a short path. There is **no APK** (the app is a Windows desktop app). The app is **not code-signed**, so Windows may warn you. Computation results and tests are not included. No data is needed: the crust is built by the calculation itself. The first run takes a few minutes (numba compiles); try the bundled small example first.

You are free to change the design documents and the code and compare the results.

---

## License

- **The author holds the copyright.**
- **The code is under the GNU General Public License v3.0 or later (GPL-3.0-or-later).** The full text is [`LICENSE`](LICENSE). **If you modify it and distribute it, you must publish the source under the same GPL-3.0-or-later terms.**
- **The design documents and the text are under the Creative Commons Attribution-ShareAlike 4.0 International license (CC BY-SA 4.0).** This covers `docs/`, `docs_en/`, the READMEs and the other written text of this repository, and the text of the matching book. See [`LICENSE-DOCS.md`](LICENSE-DOCS.md).
- **If you use them, say so.** State where it came from (the title of the book and the name of this repository) and keep the copyright notice. If you changed it, say that you changed it.
- **In this project the design documents are the source of the code.** When you publish something made from this code, **publish the design documents together with the code.**
- Third-party components (numpy, numba, matplotlib and pillow installed by `pip install .`; ffmpeg; the Flutter engine inside the EXEs) remain under their own original licenses.
- Provided "as is", without warranty — as the GPL-3.0 text says.

## 著作権とライセンス

- **著作権は、著者にあります。**
- **コードは、GNU General Public License v3.0 以降（GPL-3.0-or-later）です。**全文は [`LICENSE`](LICENSE) です。**改変して配布するときは、同じ GPL-3.0 以降の条件で、ソースを公開する義務があります。**
- **設計書と文章は、Creative Commons 表示-継承 4.0 国際（CC BY-SA 4.0）です。**このリポジトリの `docs/`・`docs_en/`・README ほかの文章と、対応する本の文章が当たります。内容は [`LICENSE-DOCS.md`](LICENSE-DOCS.md) です。
- **使ったときは、使ったことを書いてください。**どこから使ったか（本の題名と、このリポジトリの名前）と、著作権の表示を、使った先に書いてください。直したときは、直したことも書いてください。
- **このプロジェクトでは、設計書がコードの源です。**コードを使って作ったものを公開するときは、**設計書も、コードと一緒に公開してください。**
- 第三者の部品（`pip install .` で入る numpy・numba・matplotlib・pillow、ffmpeg、EXE の中の Flutter の engine）は、それぞれの元のライセンスのままです。
- 現状のまま（as is）提供します。保証はありません（GPL-3.0 の全文のとおりです）。
