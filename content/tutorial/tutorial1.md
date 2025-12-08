+++
date = '2025-10-15T13:10:14+09:00'
draft = false
title = 'Tutorial 1 - NicolNavi Basics'
+++

## 1. Overview

Work through this tutorial to learn the core NicolNavi operations using a pelitic schist microscope video. By following the steps you will complete preprocessing, grain-boundary detection, mineral labelling, and basic modal/SPO checks for a rotation video.

## 2. Prerequisites

- NicolNavi is running and the target project is open.
- You can access the sample video `nicolnavi_app/Examples/pelitic-schist-xpl.avi`.

## 3. Layout

- **Left panel**: Image viewer showing the analysed frame, boundaries, and labels.
- **Right panel**: Buttons, parameter inputs, and checkboxes for each stage.
- **Center**: `Image list` selector that swaps the map displayed on the left.

## 4. Workflow

### 4.1 Load the Video

1. Click `1 Select` on the right panel.
2. Choose `nicolnavi_app/Examples/pelitic-schist-xpl.avi` and open it.
3. Confirm that the left panel shows the first frame resized to a width of 1000 px.

<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic1.png" style="width: 30%;">

### 4.2 Run Preprocessing

1. Select `2 Start` to launch discretisation and rotation-centre estimation.
2. When the process finishes, the app switches to the rotation-centre adjustment screen.

<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic2.png" style="width: 100%;">

### 4.3 Adjust the Rotation Centre

1. Check that the red cross is centred on the concentric pattern.
2. If it is misaligned, fine-tune the coordinates with the `+` and `−` buttons. In this dataset the default position is almost correct, so you can skip adjustments.
3. Click `3 Continue` to fix the centre.

### 4.4 Review the Derived Maps

1. After the automatic transition, open `Image list` and review these representative maps.

| Map | Description |
| --- | --- |
| `color` | Brightest colours observed during a full rotation. |
| `extinction color` | Colours at the darkest instant. If the image never darkens, re-check the previous steps. |
| `R` | Pixel-level retardation values. The `Video` tab controls the retardation search range. With `max retardation = 300`, non-quartz values are indicative only. |
| `extinction angle` | Map of extinction angles for each pixel. |
| `raw image` | Unprocessed frame. Selecting, for example, $\phi = 22.5\degree$ shows the frame at that rotation angle. |

<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic3.png" style="width: 100%;">

{{< notice warning >}}
If the entire `extinction color` map remains bright, the sensor may be saturating or preprocessing was inadequate. Tutorial 2 covers remedies.
{{< /notice >}}

### 4.5 Tune Grain-Boundary Parameters

1. Set the initial parameters in the right panel for your target textures.
2. Press `6 Detect Grain Boundary` to overlay the detected boundaries.
3. Adjust `4 median filter` and `5 parameters` as shown below.
4. Click `6 Calculate grain boundaries` again to refresh the result.

<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic4.png" style="width: 30%;">

<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic5.png" style="width: 100%;">
Left: default settings. Right: after tuning.

| Parameter | Description |
| --- | --- |
| **median filter** | Smoothing window for noise suppression. Large values remove fine structure. |
| **boundary detection sensitivity** | Higher values capture finer details but increase false positives. |
| **boundary connectivity** | Maximum gap (px) treated as connected. Excessive values over-connect regions. |
| **smallest grain size** | Minimum area in `px^2`. Regions below the threshold are discarded as noise. |

{{< notice info >}}
Expect to iterate when extracting boundaries. Toggle `Show grain boundary` to inspect the overlay frequently.
{{< /notice >}}

{{< notice warning >}}
A single parameter set rarely isolates all mineral combinations. Some datasets require mineral-specific processing.
{{< /notice >}}

### 4.6 Finalise the Grain Boundaries

1. Continue adjusting until the result matches your intent.
2. Click `7 Continue` to proceed to the labelling stage.

### 4.7 Configure Labels

1. Enter `mica` in `Label Name` and press `+`. Add `bulk` in the same way.
2. Select `mica`, then click 5–10 representative mica grains in the left panel. Repeat for `bulk`.
3. If misclassifications remain, extend the training data until predictions stabilise.
4. Choose `Done` to confirm the labels. In this sample a few dozen grains are sufficient.

<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic6.png" style="width: 100%;">

### 4.8 Propagate Labels

1. Press `9 Propagate labels` to apply labels to all grains based on the training set.
2. Inspect the result. If the classification drifts, add training grains and re-run the propagation.

### 4.9 Manual Edits

1. Use `10 edit labels` to switch to manual editing.
2. Choose the desired label and click regions that require corrections.
3. Toggle `Show grain boundary` to verify the outline while editing.

### 4.10 Save the Labelling Result

1. When satisfied, select `11 Save` to store the label configuration.
2. Leaving the screen without saving discards the edits, so save before moving on.

### 4.11 Export Images (Optional)

1. Use `12 Save image` to export the current view.
2. PNG is recommended for documentation or publications.

## 5. Analyse Modal Composition

### 5.1 Histogram-Based Ratios

1. Open the `analysis` tab.
2. Select `histogram` view and choose `retardation` as the metric.
3. Use `13 minerals` to toggle mineral visibility and study the distribution.

<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic7.png" style="width: 100%;">
<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic8.png" style="width: 30%;">

{{< notice info >}}
The histogram shows the mean, standard deviation, min/max, mode, and count for each group. Use these values to interpret retardation ranges for the labelled minerals.
{{< /notice >}}

### 5.2 Rose Diagram

1. Switch the view to `rose diagram` to examine preferred orientations.
2. Enable `14 rose diagram` and keep `retardation` selected.

<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic9.png" style="width: 30%;">
<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic10.png" style="width: 100%;">

### 5.3 Orientation Stats

1. Focus on the mica alignment by selecting only the `mica` label.
2. Read the statistics in `16 information`. Example output:

```text
Mean orientation: bulk: 171.952°, mica: 171.952°
Circular variance: bulk: 0.458, mica: 0.458
```

Mean orientation indicates the SPO trend for mica. Circular variance approaches 0 for strong alignment and 1 for random orientations.

<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic12.png" style="width: 30%;">
<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic13.png" style="width: 100%;">

### 5.4 SPO View and Ellipse Approximation

1. Switch `14 rose diagram` to `SPO`.
2. Choose `ellipse` from `Image list` to display ellipse fits for each grain.

<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic14.png" style="width: 100%;">

### 5.5 Grain-Shape Scatter Plot

1. Change the view to `scatter`.
2. Set the axes to `x: ellipse major axis length` and `y: ellipse minor axis length`.
3. Use the regression line to estimate the aspect ratio—for example, `y = 0.224 x` implies ~1:3.2.

<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic15.png" style="width: 100%;">

### 5.6 Modal Composition (Area Fraction)

1. Switch to `histogram` again.
2. Enable `16 other minerals`.
3. Change the metric from `17 retardation` to `size` to plot area-based histograms.

<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic16.png" style="width: 100%;">
<img src="https://tan-furukawa.github.io/niconavi/images/page/tutorial/tutorial1/pic17.png" style="width: 100%;">

Example output:

```text
Mean: bulk: 394.808, mica: 558.211, other minerals: 383.620
Std Dev: bulk: 1807.601, mica: 493.803, other minerals: 1863.461
Min: bulk: 14.000, mica: 17.000, other minerals: 14.000
Max: bulk: 36946.000, mica: 1814.000, other minerals: 36946.000
Mode: bulk: 24.000, mica: 130.000, other minerals: 24.000
Count: bulk: 593, mica: 38, other minerals: 555
Integral ratio: mica: 9.06%, other minerals: 90.94%
Count ratio: mica: 6.41%, other minerals: 93.59%
```

`Integral ratio` gives the area fraction based on the histogram integral. In this example mica constitutes about 9.1%.

## 6. Wrap-Up

- Following these steps covers preprocessing, boundary detection, labelling, and structural analysis for a rotation video.
- Expect to iterate between boundary detection and label propagation. Rebalance parameters and training data if the result is unstable.
- Always verify the outputs via `information` statistics and plots, and cross-check them with the imaging and sample conditions.
