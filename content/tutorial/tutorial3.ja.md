+++
date = '2026-10-21T00:00:00+09:00'
draft = false
title = 'Tutorial 3 - 石英薄片から c 軸方位を求める'
+++

このチュートリアルでは、サンプルデータ `ggg3` を使い、動画の読み込みから粒界の抽出、鉱物相のラベル付け、CPO（結晶方位選択配向）の表示までを順に行います。

## 1. サンプルデータを準備する

[NicoNavi の `ggg3` サンプルデータ](https://github.com/Tan-Furukawa/niconavi/tree/main/examples)を開き、フォルダー内の5本の動画をダウンロードしてください。

## 2. 動画と測定条件を入力する

NicoNavi を起動し、右側の **Images** パネルで次の項目を設定します。画像内の青い番号と、以下の番号が対応しています。

{{< img src="images/page/tutorial/01-input-settings.png" alt="Imagesパネルで動画と測定条件を入力する画面" >}}

1. **Rotated XPL** に、直交ニコルでステージを回転させた動画を指定します。
2. **Thin section thickness** に薄片の厚さを入力します。今回の薄片は `0.022 mm` です。厚さが厳密に測定できていなくても、後述の補正を利用できるため、結晶方位の測定に大きな問題はありません。
3. **Rotated XPL + λ plate** に、鋭敏色検板を挿入してステージを回転させた動画を指定します。
4. **λ** に鋭敏色検板の位相差を入力します。
5. **0° tilted image** に、0°方向へ傾けた動画を指定します。
6. **45° tilted image** に、45°方向へ傾けた動画を指定します。
7. **45° reference image** に、45°傾斜用の参照動画を指定します。
8. 動画のホワイトバランスが未調整の場合は、**Gray-world white balance** をオンにします。今回のサンプル動画は未調整なので、チェックを入れてください。

{{< notice info >}}
このチュートリアルで使う5本の動画は、手順1でダウンロードした `ggg3` フォルダーに含まれています。
{{< /notice >}}

すべての入力が終わったら、**Start** をクリックします（画像の9）。

{{< img src="images/page/tutorial/02-start.png" alt="入力完了後にStartを押す画面" >}}

## 3. 回転中心を確認する

**Center** タブでは、画像に見える同心円状のパターンから回転中心を決めます。赤い「＋」が同心円の中心にあれば問題ありません。

中心は自動検出されますが、ずれている場合は **X** と **Y** の値を調整して手動で直してください。今回のサンプルでは最初から中心が合っているため、そのまま **Continue** をクリックします（画像の10）。

{{< img src="images/page/tutorial/03-center.png" alt="同心円の中心と赤い十字を確認するCenterタブ" >}}

## 4. 計算結果の品質を確認する

**Map** タブを開き、まず赤色で示した3つの画像切り替えボタンを確認します。ここでは、動画どうしの位置合わせと、回転動画の角度推定が正しいかを点検します。

{{< img src="images/page/tutorial/04-quality-buttons.png" alt="品質確認に使うextinction colorとoriginal color changeのボタン" >}}

1. **extinction color**：各ピクセルが最も暗くなったときの色を表示します。正常なら、常に暗い粒界を除いて粒内はおおむね黒くなります。白飛びや回転中心のずれがあると、粒内まで明るく、ざらついた見え方になります。
2. **original color change (0°)**：回転動画と0°傾斜動画の位置合わせを確認します。
3. **original color change (45°)**：回転動画と45°傾斜動画の位置合わせを確認します。画像の一部が欠けて見えること自体は正常です。

位置合わせがずれている場合、**original color change** では粒界付近に赤・緑・青などの鮮やかな色が強く現れる傾向があります。次の比較画像では、左列が正常、右列が失敗例です。失敗例の **extinction color** は回転中心がずれており、粒界以外も明るく、ざらついています。

{{< img src="images/page/tutorial/05-quality-comparison.png" width="80%" alt="品質確認画像の正常例と失敗例の比較" >}}

## 5. 角度マップを整え、粒界を抽出する

**Angle map**（画像の1）へ戻り、次の順で処理します。

{{< img src="images/page/tutorial/06-segmentation.png" alt="Angle mapでClean、Segment、Fill、Applyを実行する画面" >}}

1. **Clean**（画像の2）を10回程度クリックします。これは画像のノイズを除く処理です。クリックするたびに角度マップが徐々に滑らかになる様子を確認できます。
2. **Segment**（画像の3）をクリックします。隣接する superpixel 間の c 軸のなす角が指定値以下なら、それらを同じ領域として結合します。その結果、隣り合う粒子間の方位差が設定した角度以上になるように分割されます。
3. **Fill**（画像の4）を、表示値が `5 px` になるまでクリックします。これは、常に消光して黒く見える細い粒界領域を周囲の相へ統合する処理です。目安は `5 px` です。
4. **Apply**（画像の5）をクリックして粒界を計算します。

粒界が表示されたら結果を確認し、**Continue**（画像の6）をクリックします。

{{< img src="images/page/tutorial/07-boundaries.png" alt="粒界抽出後にContinueを押す画面" >}}

## 6. 鉱物相をラベル付けする

今回はすべての粒子を石英として扱います。

1. **Labels** の入力欄に `Quartz` と入力します（画像の1）。
2. **＋** ボタンをクリックします（画像の2）。
3. 左側の画像内をクリックします（画像の3）。

{{< img src="images/page/tutorial/08-label-quartz.png" alt="Quartzラベルを追加して画像をクリックする画面" >}}

画像全体が石英として分類されたら完了です。**Save**（画像の4）をクリックして、次の工程へ進みます。

{{< img src="images/page/tutorial/09-label-complete.png" alt="すべての粒子をQuartzとして分類した画面" >}}

複数の鉱物を区別したい場合は、必要な鉱物名を **Labels** に追加し、それぞれの相を分類できます。

## 7. CPOを計算する

**Analysis** タブへ移動し、解析の選択欄（画像の1）から **CPO**（画像の2）を選びます。

{{< img src="images/page/tutorial/10-analysis-cpo.png" alt="AnalysisタブでCPOを選択する画面" >}}

**Normalize to 90°** は、レタデーションが指定した **Percentile** 以上の相を90°として正規化する機能です。薄片厚さを厳密に測定できていない場合にも利用できますが、特別な理由がなければ初期設定のままで構いません。

**Calculate**（画像の3）をクリックし、計算が終わるまで待ちます。

{{< img src="images/page/tutorial/11-calculate-cpo.png" alt="CPOのCalculateボタンを押す画面" >}}

## 8. 結果を表示し、読み取る

計算が終わったら **φ=0–360°**（画像の4）をクリックします。石英の c 軸方位が方位マップとして表示されます。

{{< img src="images/page/tutorial/12-show-results.png" alt="φ=0–360°のCPO計算結果を表示した画面" >}}

### 極図

極図は、測定領域に含まれる c 軸方位の分布をまとめて表示します。同じ計算結果でも、表示形式やデザインを変更できます。

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 2rem; align-items: start;">
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial/13-polar-plot.png" width="100%" alt="c軸方位を示す標準表示の極図" >}}
    <figcaption><strong>標準表示：</strong>方位ごとの頻度を棒の長さで読み取ります。棒が集中する方向ほど、その方向を向く c 軸が多いことを示します。</figcaption>
  </figure>
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial/14-polar-plot-styled.png" width="100%" alt="デザインを変更したc軸方位の極図" >}}
    <figcaption><strong>デザイン変更例：</strong>同じ方位データの見せ方を変更した例です。解析結果に応じて、比較しやすい表示形式を選べます。</figcaption>
  </figure>
</div>

### 方位マップ

方位マップでは、薄片上の各粒子について、c 軸がどの方向を向いているかを色で確認できます。

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 2rem; align-items: start;">
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial/15-map-0-360.png" width="100%" alt="傾斜情報を含むφ=0–360°の方位マップ" >}}
    <figcaption><strong>φ=0–360°：</strong>傾斜動画の情報を含めて推定した結果です。c 軸の向きを360°の範囲で表現できます。</figcaption>
  </figure>
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial/16-map-0-180.png" width="100%" alt="傾斜情報を使わないφ=0–180°の方位マップ" >}}
    <figcaption><strong>φ=0–180°：</strong>傾斜動画の情報を使わずに導出した結果です。傾斜情報の推定は難しいため、左の φ=0–360° はこの結果よりも色が細かく入り混じり、ややばらつきが大きく見えます。</figcaption>
  </figure>
</div>
