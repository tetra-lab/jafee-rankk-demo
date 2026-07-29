# δ_Σ マッピング デモアプリ

学会発表（JAFEE 2026-08-09）用のライブデモ。`analysis_ccc.ipynb` / `analysis_dcc.ipynb` / `analysis_adcc.ipynb` の
Section 3 で行っている δ_Σ マッピング分析（理論的上界 B(k) = T̄(k) + δ_Σ·C̄(k) を最小化する k と、
walk-forward 実証で最良だった `wf_best_k` の一致区間を探す分析）を、その場で δ_Σ を動かしながら確認できる。

## 公開URL（GitHub Pages）

**<https://tetra-lab.github.io/jafee-rankk-demo/>**

このURLをブラウザで開けばそのまま動く（末尾のスラッシュまで含めてアクセスする）。

> **注意：よくある間違い**
>
> | URL | 結果 |
> |---|---|
> | `https://tetra-lab.github.io/jafee-rankk-demo/` | ✅ 正しい |
> | `.../jafee-rankk-demo/delta_sigma_demo.html` | ❌ 404 — 公開時に `index.html` へ改名済み。ローカルのファイル名では開けない |
> | `.../JAFEE-rankk-demo/` | ❌ 404 — URLは大文字小文字を区別する |
> | `github.com/tetra-lab/jafee-rankk-demo/blob/main/index.html` | ⚠️ ソースが表示されるだけでアプリは動かない |

## 使い方

- **公開版:** 上記URLを開く（リポジトリ上のファイル名は `index.html`）
- **ローカル版:** このディレクトリの `delta_sigma_demo.html` をブラウザ（Chrome / Safari 等）でダブルクリック

どちらもネットワーク接続不要、外部ライブラリ不要（単一HTMLファイルに全データ・全ロジックを内包）。
公開版とローカル版は同一内容（ファイル名のみ異なる）。

- 上部タブでモデル（CCC / DCC / ADCC）とデータセット（df1 / df2）を切り替え
- δ_Σ スライダーを動かすと、3つのグラフと数値パネルがリアルタイムに更新される
  - (a) δ_Σ vs theoretical_k の階段関数（`plot_delta_sigma_wf_mapping` 相当）
  - (b) 現在の δ_Σ での B(k) 棒グラフ
  - (c) T(k)・C(k) の推移

## データソース

`今回の研究/analysis_results.json` の `summary_k`（各 k の T(k), C(k)）、`wf_best_k`、`delta_range` 等を
そのまま埋め込んでおり、再計算は行っていない。B(k) の計算とその場での argmin だけをブラウザ上の
JavaScript で行う（`mgarch_rankk_common.py` の `select_theoretical_k_from_summary` と同じロジック）。

**注意:** 本研究の理論選択では k=0（逆分散ベースライン）を候補から除外している
（`analysis_results.json` の `theoretical_k_at_delta_max` 等の記録値と整合させるための挙動）。
棒グラフでは k=0 を灰色・`k=0*` 表記で参照値として表示するが、theoretical_k の argmin には含めない。
