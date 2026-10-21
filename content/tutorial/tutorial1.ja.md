+++
date = '2026-10-21T00:00:00+09:00'
draft = false
title = 'Tutorial 1 - 回転動画1本から Angle map を作る'
+++

このチュートリアルでは、化石を含む薄片のサンプルデータ `orikabetoge` を使います。直交ニコル下でステージを回転させた動画1本だけを読み込み、c 軸方位を色で示す **Angle map** と、化石の形を観察しやすい **Maximum intensity image** を表示します。

## 1. サンプル動画を準備する

[NicoNavi の `orikabetoge` サンプルデータ](https://github.com/Tan-Furukawa/niconavi/tree/main/examples/orikabetoge)を開き、`orikabetoge_xpl.avi` をダウンロードしてください。

## 2. 動画と薄片厚さを入力する

NicoNavi を起動し、右側の **Images** パネルで次の項目を設定します。画像内の青い番号と以下の番号が対応しています。

{{< img src="images/page/tutorial1/01-input.png" alt="Rotated XPL動画、薄片厚さ、ホワイトバランスを設定する画面" >}}

1. **Rotated XPL** の **Select** を押し、直交ニコル下でステージを回転させた動画 `orikabetoge_xpl.avi` を選びます。この動画だけが必須で、ほかの動画はすべてオプションです。
2. **Thin section thickness** に薄片の厚さ `0.04 mm` を入力します。厚さを入力すると、その下の **Maximum retardation**（最大レタデーション）が自動計算されます。
3. 動画のホワイトバランスが未調整の場合は **Gray-world white balance** にチェックを入れます。今回の動画は未調整なので、チェックを入れてください。

今回は **Rotated XPL + λ plate** と **XPL + λ plate (0°/45°)** の画像は使用しません。これらの入力で何ができるようになるかは、最後に説明します。

動画を選ぶと、左側に1フレーム目が表示されます。リング状に光っている部分が化石です。入力を確認したら **Start**（画像の4）を押して計算を始めます。

{{< img src="images/page/tutorial1/02-preview-start.png" alt="化石を含む動画の1フレーム目を確認してStartを押す画面" >}}

## 3. 回転中心を確認する

**Center** タブには、動画の全フレームを重ね合わせて得られた同心円状のパターンが表示されます。この同心円の中心が、ステージの回転中心です。赤い「＋」が同心円の中心に重なっていれば問題ありません。

中心は自動検出されますが、ずれている場合は **X**、**Y** の −／＋ボタンを押すか、数値を直接入力して調整してください。今回は最初から中心が合っているため、そのまま **Continue** を押します。

{{< img src="images/page/tutorial1/03-center.png" alt="同心円パターンと赤い十字で回転中心を確認するCenterタブ" >}}

## 4. Angle map を読み取る

計算が終わると **Map** タブへ移動し、**Angle map** が表示されます。

{{< img src="images/page/tutorial1/04-angle-map.png" alt="化石薄片のAngle mapと画像切り替えボタン" >}}

Angle map は、**Video** タブで入力した薄片厚さを参考に推定した c 軸の傾き（inclination、0–90°）と、消光角を組み合わせた画像です。右上のカラーチャートが色と角度の対応を示し、θ が inclination、φ が消光角を表します。

Angle map は、角度情報を定性的に観察したいときに便利です。この例では、化石の殻に沿って色が変化していることから、殻を構成する結晶の向きが場所によってどのように変わるかを確認できます。

続いて、画像内の次のボタンを順に確認します。

1. **Images > Maximum intensity image**
2. **Images > extinction color**（赤色のボタン）

## 5. extinction color で計算品質を確認する

**extinction color** は、各ピクセルが最も暗くなる、つまり消光するときの色を表示します。回転中心などが正しく推定できていれば、次のように画像全体がほぼ黒くなります。

{{< img src="images/page/tutorial1/05-extinction-color.png" alt="正常に計算され全体がほぼ黒く表示されたextinction color画像" >}}

この表示は、回転中心の推定や計算結果が妥当かを確認するために使います。うまく計算できていない場合の見え方は Tutorial 2 で説明します。

## 6. Maximum intensity image で化石を観察する

**Maximum intensity image** は、各ピクセルが最も明るくなる角度、すなわち消光角＋45°での色を表示します。どの向きの結晶も明るく写るため、化石の形が分かりやすくなります。

{{< img src="images/page/tutorial1/06-maximum-intensity.png" alt="化石の形が見やすいMaximum intensity image" >}}

**raw image > φ=0°** と切り替えて比較すると、Maximum intensity image の特徴を確認しやすくなります。

## 7. 動画1本で分かること・分からないこと

直交ニコル下の回転動画1本だけで、Angle map と Maximum intensity image を表示できます。ただし、ステージを1周させる間に消光が4回起こるため、次の向きは区別できません。

- azimuth（c 軸の方位）が 0–90° と 90–180° のどちらにあるか
- inclination（c 軸の傾き）が 0–90° と 90–180° のどちらにあるか、つまり c 軸が上向きか下向きか

これらの不定性を解消したい場合は、**Video** タブで追加の動画・画像を読み込みます。

- **Rotated XPL + λ plate**：鋭敏色板を入れて回転させた動画を追加すると、azimuth の不定性を解消できます。
- **XPL + λ plate (0°/45°)**：tilt ステージを使って撮影した画像を追加すると、inclination の不定性を解消できます。

これらの入力を使った解析は、Tutorial 2 と Tutorial 3 で扱います。
