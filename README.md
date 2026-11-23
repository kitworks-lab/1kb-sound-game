# 1KB Sound Game (1,018-Byte Single-File HTML5 Arcade)

**Play Live Demo:** https://kitworks-lab.github.io/1kb-sound-game/

外部ファイル0個・生のUTF-8サイズ **1,018 バイト**（1KB = 1,024B 以内・残り6B）の単一HTMLファイルで動く、Canvas 2D描画＋Web Audio API 8bit矩形波シンセ搭載のアーケードゲーム（1KB DODGE）実験リポジトリです。

A playable retro paper-ink Canvas 2D arcade game with synthesized 8-bit Web Audio sound effects packed into a single raw **1,018-byte** HTML file (under 1 KB / 1,024 bytes, zero external dependencies, zero audio files).

---

## Compression Milestones / 圧縮マイルストーン

| Stage | File | Raw Size (UTF-8) | Notes |
| --- | --- | ---: | --- |
| Baseline | [`v1_readable.html`](v1_readable.html) | **3,306 B** | Readable Canvas + Web Audio prototype / 可読版プロトタイプ |
| Compact | [`v2_compact.html`](v2_compact.html) | **1,493 B** | Stripped HTML boilerplate, shortened identifiers / 定型タグ削除・短縮版 |
| Final | [`index.html`](index.html) | **1,018 B** | **-69.2%** vs v1 (6 B spare under 1,024 B) / 1KB突破・公開版 |

---

## 日本語 (JP)

### 遊び方・操作方法
- **移動**: キーボードの左右矢印キー（`←` / `→`）または **マウス移動**（キャンバス内）
- **ルール**: 赤い隕石を回避するとスコア加算（`+1`）、緑のコインを取るとボーナス（`+10`）＋徐々に加速
- **リスタート**: ゲームオーバー画面で **Spaceキー**（または任意のキー） / **クリック**
- **サウンド（Web Audio API 矩形波・音声ファイル0個）**: コイン取得 `880 Hz` / 被弾 `120 Hz` / リスタート `523 Hz`（初回操作時に `AudioContext` を起動）

### 1,018バイトに収めた主なテクニック
- **HTML5省略タグ＋暗黙グローバル**: `DOCTYPE` / `html` / `head` / `style` / 閉じタグを削り、`<canvas id=c>` の暗黙グローバル `c` とタグ付きテンプレート ``c.getContext`2d` `` を利用
- **139バイト Web Audio 矩形波シンセ**: 二重 `with` 文で `AudioContext` と `OscillatorNode` を1関数に圧縮し、MP3/WAVなしで3音を生成
- **多態描画関数 `r()`＋`m*V` 統合ループ**: 第5引数の有無で `fillRect` / `fillText` を兼用し、`filter()` 1周の中で移動・描画・当たり判定・ゲームオーバー時の自動凍結まで処理

### 正直な弱点・割り切り
- 圧縮優先のため `with` 文・暗黙グローバル・非推奨の `KeyboardEvent.which` を使っており、実務の本番コードには非推奨です
- タッチ操作・一時停止・音量ミュート・`localStorage` での永続ハイスコア保存は1KB枠の都合で省いています

---

## English (EN)

### Controls & Gameplay
- **Move**: Left / Right **Arrow keys** (`←` / `→`) or **Mouse** across the canvas
- **Goal**: Dodge falling red meteors (`+1` point each) and catch green coins (`+10` points) as fall speed ramps up
- **Restart**: Press **Space** (or any key) / **Click** on the Game Over overlay
- **Synthesized Audio (0 audio files)**: Web Audio API square-wave synth firing `880 Hz` (coin), `120 Hz` (hit), and `523 Hz` (restart)

### Key 1 KB Compression Techniques
- **Minimal HTML5 & Implicit Globals**: Omitted `DOCTYPE`, `<html>`, `<head>`, and closing tags; relied on implicit element global `c` (`<canvas id=c>`) and tagged template ``c.getContext`2d` ``
- **139-Byte Web Audio Synth**: Nested `with` blocks over `AudioContext` and `OscillatorNode` to generate 8-bit square-wave tones with zero audio assets
- **Polymorphic `r()` + Single `filter()` Loop**: One helper dispatches `fillRect` vs. `fillText` by arity, while `m*V` freezes entity motion on Game Over inside a single update/render pass

### Honest Trade-Offs
- Uses code-golf idioms (`with`, implicit globals, legacy `event.which`) strictly for the 1,024-byte challenge — not recommended for production apps.
- Touch controls, pause/mute toggles, and persistent `localStorage` high scores were traded off to stay strictly under 1,024 bytes.

---

## KitWorks Lab

- **Live Demos & OBS Widgets**: https://kitworks-lab.github.io/
- **BOOTH (JP)**: https://kitworks.booth.pm/
- **Gumroad (EN / Global)**: https://earnbot7.gumroad.com/
- **YouTube Channel**: https://www.youtube.com/channel/UC_r4xzn2zs3gjbU3rXn3lpA

## License

MIT License — see [LICENSE](LICENSE).
