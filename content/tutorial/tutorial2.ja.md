+++
date = '2026-10-21T00:00:00+09:00'
draft = false
title = 'Tutorial 2 - 複数の鉱物相を分類して SPO・CPO を解析する'
+++

このチュートリアルでは `ym3-2` の回転動画を使い、粒界の抽出、石英・雲母・その他の3相への分類、粒子形状の選択配向（SPO）、石英 c 軸の結晶方位選択配向（CPO）を順に解析します。傾斜画像を使わなくても、c 軸方位を 0–180° の範囲で求められます。

## 1. 動画と測定条件を入力する

NicoNavi を起動し、右側の **Images** パネルに動画と測定条件を入力します。画像内の青い番号と次の番号が対応しています。

{{< img src="images/page/tutorial2/01-input.png" alt="Imagesパネルで回転動画と測定条件を入力する画面" >}}

1. **Rotated XPL** の **Select** を押し、直交ニコル下でステージを回転させた動画 `ym3-2_xpl.avi` を選びます。この動画は必須です。
2. **Thin section thickness** に薄片の厚さ `0.03 mm` を入力します。厚さが正確でなくても、CPO 計算時の **Normalize to 90°** で補正できるため、大きな問題はありません。
3. **Rotated XPL + λ plate** の **Select** を押し、鋭敏色板を入れてステージを回転させた動画 `ym3-2_lambda.avi` を選びます。
4. **λ** に鋭敏色板の位相差 `530 nm` を入力します。
5. 今回の動画はホワイトバランスが未調整なので、**Gray-world white balance** にチェックを入れます。

**0° tilted image**、**45° tilted image**、**45° reference image** はオプションです。今回は使用しません。この場合も解析できますが、c 軸の上下を区別する φ=0–360° の情報は得られません。

動画を選ぶと、左側に1フレーム目が表示されます。**Images** の **xpl** と **xpl+λ** で表示する動画を切り替えられます。入力を確認したら **Start**（画像の6）を押します。

{{< img src="images/page/tutorial2/02-video-preview.png" alt="読み込んだ動画のフレームを確認してStartを押す画面" >}}

## 2. 回転中心を確認する

**Center** タブでは、同心円状の模様の中心に赤い「＋」が重なっているか確認します。ずれている場合は **X**、**Y** の −／＋ボタンで調整してください。今回は最初から合っているため、そのまま **Continue**（画像の7）を押します。

{{< img src="images/page/tutorial2/03-center.png" alt="同心円の中心と赤い十字を確認するCenterタブ" >}}

## 3. 消光画像で計算品質を確認する

**Map** タブを開き、**Images** の赤い **extinction color** ボタン（画像の1）を押します。この画像は各ピクセルが最も暗くなった時点の色を示し、画像の位置合わせや回転角度の推定が正しいかを確認するために使います。

{{< img src="images/page/tutorial2/04-extinction-check.png" alt="Mapタブでextinction colorを表示する画面" >}}

正常な結果では、粒界を除く粒内のほとんどが黒くなります。粒界は一般に完全には黒くならず、明るく残ります。白飛びしていたり回転中心がずれていたりすると、粒内まで明るく、ざらついて見えます。

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(210px, 1fr)); gap: 1.5rem; align-items: start;">
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial2/quality-correct.png" width="100%" alt="回転中心と露出が適切な正常例" >}}
    <figcaption><strong>正常：</strong>粒内が暗く、主に粒界が明るく見えます。</figcaption>
  </figure>
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial2/quality-overexposed.png" width="100%" alt="白飛びした消光画像の失敗例" >}}
    <figcaption><strong>白飛び：</strong>粒内にも明るい部分が残ります。</figcaption>
  </figure>
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial2/quality-center-shifted.png" width="100%" alt="回転中心が右にずれた消光画像の失敗例" >}}
    <figcaption><strong>中心ずれ：</strong>粒界以外も明るく、ざらついて見えます。</figcaption>
  </figure>
</div>

## 4. 角度マップを整え、粒界を抽出する

**Angle map**（画像の1）に戻り、次の順に処理します。

{{< img src="images/page/tutorial2/05-angle-clean.png" alt="Angle mapでClean、Segment、Fill、Applyを実行する画面" >}}

1. **Clean**（画像の2）を10回程度押します。画像ノイズが除去され、角度マップが徐々に滑らかになる様子を確認できます。
2. **Segment**（画像の3）を押します。隣接する superpixel 間の c 軸のなす角が指定値以下なら、それらを同じ領域として結合します。その結果、隣り合う粒子の方位差が設定角度以上になるように分割されます。
3. **Fill**（画像の4）を、表示値が `5 px` になるまで押します。常に消光して黒く見える細い粒界領域のうち、指定幅以下のものを周囲の相へ統合します。`5 px` 程度が目安です。
4. **Apply**（画像の5）を押して粒界を計算します。

粒子ごとに色分けされた **grain map > grains** が表示されたら、結果を確認して **Continue**（画像の7）を押します。

{{< img src="images/page/tutorial2/06-grains.png" alt="粒子ごとに色分けされたgrain mapとContinueボタン" >}}

## 5. 石英・雲母・その他を分類する

今回は粒子を **Quartz**（石英）、**Mica**（雲母）、**Other**（その他）の3つに分けます。

1. **Label name**（画像の1）に鉱物名を入力します。
2. **＋**（画像の2）を押してラベルを追加します。この操作を `Quartz`、`Mica`、`Other` の3回繰り返します。ラベル名は任意ですが、このチュートリアルでは以降この3つを使用します。

{{< img src="images/page/tutorial2/07-labels-add.png" alt="Filterタブで鉱物ラベルを追加する画面" >}}

分類したいラベルの丸ボタンを選び（画像の3）、左側の画像で、その鉱物に該当する粒子をクリックします（画像の4）。雲母は干渉色が鮮やかで細長い粒子を目安に選びます。すべての粒子を手作業で選ぶ必要はなく、代表的な粒子を見本として数個選べば十分です。

{{< img src="images/page/tutorial2/08-label-mica.png" alt="Micaラベルを選び見本となる雲母粒子をクリックする画面" >}}

クリックした見本は赤枠で囲まれます。まだ Mica の見本しか与えていない段階では、すべての粒子が Mica（緑）と予測されます。

{{< img src="images/page/tutorial2/09-label-mica-only.png" alt="Micaの教師データだけを入力した途中段階" >}}

同じように Quartz と Other の見本も追加します。見本をもとに残りの粒子が自動分類され、石英は青、雲母は緑、その他はオレンジで表示されます。誤分類された粒子があれば、正しいラベルを選んでその粒子をクリックし、見本を追加してください。

**Opacity**（画像の5）では分類色の重ね合わせの濃さを調整できます。右へ動かすと色が濃くなり、左へ動かすと下の薄片画像を確認しやすくなります。**Learning features** の「＋」を開くと、分類に使う特徴（色、細長さ、大きさ、位置）を選べます。色に特徴がある鉱物なら **Color** を有効にする、といった調整が可能ですが、今回は初期設定を使います。

{{< img src="images/page/tutorial2/10-label-classified.png" alt="Quartz、Mica、Otherに自動分類された粒子" >}}

分類を確認したら **Save**（画像の6）を押します。**Result** には入力した見本の数と分類された粒子数が表示されます。この例では75個の教師データを入力しています。**Save** が見えない場合は、右側のパネルを下へスクロールしてください。

{{< img src="images/page/tutorial2/11-label-save.png" alt="分類結果をSaveする画面" >}}

## 6. ローズダイアグラムで SPO と方位角を比較する

**Analysis** タブに移動し、1つ目のドロップダウン（画像の1）から **rose diagram** を選びます。

{{< img src="images/page/tutorial2/12-analysis-type.png" alt="Analysisタブでrose diagramを選ぶ画面" >}}

2つ目のドロップダウン（画像の2）から **shape preferred orientation** を選ぶと、粒子形状の長軸方向（SPO）のローズダイアグラムを表示できます。相のチェックボックス（画像の3、4）で **Mica** と **Other** を外すと、石英だけの SPO になります。

**Information** には平均方向（Mean orientation）と円分散（Circular variance）が表示されます。円分散は0に近いほど、粒子の向きがよくそろっていることを示します。**Flip** は図の向きを反転し、**Opacity** は棒の透明度、**Bins** は棒の本数を変更します。いずれも表示だけの設定で、計算結果は変わりません。

{{< img src="images/page/tutorial2/13-spo-quartz.png" alt="石英だけを表示したSPOローズダイアグラム" >}}

Mica だけにチェックを入れると、相ごとの配向を比較できます。この例では雲母の円分散が `0.228`、石英が `0.620` で、雲母の方がよくそろっています。

{{< img src="images/page/tutorial2/14-spo-mica.png" alt="雲母だけを表示したSPOローズダイアグラム" >}}

2つ目のドロップダウンから **azimuth**（画像の5）を選ぶと、c 軸方位角のローズダイアグラムになります。**Grain value** では、各粒子を代表する値に中央値（Median）または平均値（Mean）を選べます。

{{< img src="images/page/tutorial2/15-azimuth.png" alt="c軸方位角のローズダイアグラム" >}}

## 7. 粒子形状と相の分布をマップで確認する

1つ目のドロップダウンから **SPO**（画像の6）を選ぶと、粒子の長軸方向を色で示したマップが表示されます。Mica と Other にもチェックを入れ（画像の7、8）、**Images > ellipse**（画像の9）を押します。

{{< img src="images/page/tutorial2/16-spo-map.png" alt="SPOマップで全相を選択してellipseを表示する手順" >}}

各粒子を楕円近似した結果が、石英＝青、雲母＝緑、その他＝オレンジで表示されます。**ellipse (major axis)** を選ぶと楕円の長軸だけを表示できます。

{{< img src="images/page/tutorial2/17-ellipses-all.png" alt="全相の粒子を楕円近似して表示した画面" >}}

Mica と Other のチェックを外す（画像の10、11）と、石英の楕円だけを表示できます。そのまま **Map** タブ（画像の12）へ移動します。

{{< img src="images/page/tutorial2/18-ellipses-quartz.png" alt="石英だけの楕円を表示してMapタブへ移る画面" >}}

**Images > Maximum intensity image**（画像の13）を押すと、各ピクセルについて最も明るくなる角度（消光角＋45°）での色を表示します。雲母とその他はチェックを外しているため黒く抜け、石英だけが表示されます。相の表示・非表示は、すべてのタブで連動します。

{{< img src="images/page/tutorial2/19-max-intensity.png" alt="石英だけを表示したMaximum intensity image" >}}

## 8. 石英の CPO を計算する

**Analysis** タブへ戻り、1つ目のドロップダウンから **CPO**（画像の14）を選びます。表示されている屈折率（ω、ε）は石英用なので、石英を解析する今回は変更しません。

**Normalize to 90°** は、レタデーションが **Percentile** 以上の相を90°とみなして正規化する機能です。薄片厚さの誤差を補正できますが、特別な理由がなければ初期設定のままで構いません。**Calculate**（画像の15）を押し、計算が終わるまで待ちます。

{{< img src="images/page/tutorial2/20-cpo-settings.png" alt="CPOの設定を確認してCalculateを押す画面" >}}

計算後、**map coi > φ=0–180°**（画像の16）を押すと、c 軸方位を色で示す方位マップが表示されます。右上のカラーホイールは色と方位の対応を示します。

**Information** に「CPO computed, but ...」と表示されるのは、傾斜画像を入力していないためです。今回は φ=0–360° の結果は得られませんが、φ=0–180° は鋭敏色板入りの回転動画から計算できます。

続いて **polar plot > φ=0–180°**（画像の17）を押します。

{{< img src="images/page/tutorial2/21-cpo-map.png" alt="傾斜画像なしで計算したφ=0–180度のc軸方位マップ" >}}

c 軸の極図（密度分布）が表示されます。**Group by** では粒子ごと（Grain）またはピクセルごと（Pixel）の集計を選べます。極図の下半分が空白なのは、c 軸の上下を判別する傾斜画像を使用していないためです。

{{< img src="images/page/tutorial2/22-polar-plot.png" alt="傾斜画像なしで計算したc軸の極図" >}}

## 9. プロジェクトと結果を保存する

右上のメニュー（≡）から、プロジェクトや解析結果を保存・出力できます。

{{< img src="images/page/tutorial2/23-export-menu.png" width="35%" alt="保存と出力のメニュー" >}}

- **Save project**：入力ファイル、設定、計算結果をプロジェクトファイルとして保存します。
- **Load project**：保存したプロジェクトを読み込みます。
- **Export image (PDF)**：現在、左側に表示している画像を PDF で出力します。
- **Export grain data**：粒子ごとの計算結果を表として出力します。
