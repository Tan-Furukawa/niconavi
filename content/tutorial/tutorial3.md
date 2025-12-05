+++
date = '2025-10-15T13:10:14+09:00'
draft = false
title = 'Tutorial 3 - Crystal Orientation Analysis'
+++

## 1. Overview

Use this tutorial to learn the NicolNavi workflow for crystallographic preferred orientation (CPO) analysis with a polycrystalline quartz sample. Building on Tutorials 1 and 2, you will combine multiple rotation videos, estimate quartz c-axis orientations, and review the results with pole figures and COI maps.

## 2. Prerequisites

- NicolNavi is running with the target project open.
- You can access the sample videos under `nicolnavi_app/Examples/cpo/`.
- You have completed Tutorials 1 and 2 (preprocessing, boundary detection, labelling).
- **CPO analysis requires significant memory. Use a computer with at least 16 GB RAM; lower-spec systems may halt mid-process.**

## 3. Video Set

NicolNavi's CPO workflow consumes five videos. Refer to the Data Acquisition page for filming details.

| Capture condition | Filename | Purpose |
| --- | --- | --- |
| XPL Rotated | `XPL.avi` | 360° rotation under crossed Nicols |
| XPL + λ-Plate Rotated | `XPL-lambda.avi` | Rotation with the first-order red plate inserted |
| XPL + λ-Plate 0° tilt | `0deg-tilt.avi` | Tilted section at 0° while sweeping the focus |
| XPL + λ-Plate 45° tilt | `45deg-tilt.avi` | Tilted section at 45° while sweeping the focus |
| XPL + λ-Plate 45° (no tilt) | `45deg-not-tilt.avi` | Short clip at 45° with the section kept horizontal |

## 4. Workflow

### 4.1 Load Videos and Set Retardation

1. In the `map` tab, click `Select` beside `XPL Rotated` and choose `Examples/cpo/XPL.avi`.
2. Repeat for the remaining inputs (`XPL-lambda.avi`, `0deg-tilt.avi`, `45deg-tilt.avi`, `45deg-not-tilt.avi`).
3. After all files are loaded, set `max retardation` in the `XPL Rotated` section. Use the highest quartz retardation expected in the sample; the default 300 nm works here and is sufficient for c-axis estimation. You will refine the value later if needed.

{{< notice info >}}
This `max retardation` guides extinction-angle and retardation estimates during preprocessing.
{{< /notice >}}

{{< notice warning >}}
Entering values above 300 nm increases the risk of failing to resolve c-axis inclinations. Keep the value at or below 300 nm when you intend to calculate orientations, and prepare thin sections so that quartz retardation stays within that range.
{{< /notice >}}

<img src="{{ "/images/page/tutorial/tutorial3/pic1.png" | relURL }}" style="width: 30%;">

### 4.2 Preprocess and Check the Rotation Centre

1. Click `Start` to begin discretisation and reference image generation. Processing takes longer than in Tutorials 1 and 2.
2. On the rotation-centre screen, confirm that the red cross aligns with the concentric pattern. For this dataset the automatic position is adequate, so you can continue without adjustment.

### 4.3 Tune Grain-Boundary Parameters

1. Return to the `map` tab and run `Detect Grain Boundary`.
2. Increase the `median filter` slider by one step and adjust the other sensitivity controls as shown below.
3. Click `Calculate grain boundaries` to update the mask. Once satisfied, choose `Continue` to enter the labelling stage.

<img src="{{ "/images/page/tutorial/tutorial3/pic2.png" | relURL }}" style="width: 30%;">

### 4.4 Assign Labels

1. The goal is to compare the quartz vein with the surrounding single crystals. Add `single crystal quartz` and `vein quartz` as label names.
2. Select each label in turn and click the corresponding grains on the left panel. In this example 17 grains were labelled, but the required number varies by dataset.
3. Expand the training set if misclassifications remain. When the preview stabilises, click `Done`.

<img src="{{ "/images/page/tutorial/tutorial3/pic3.png" | relURL }}" style="width: 100%;">

### 4.5 Run CPO Analysis

1. Switch to the `analysis` tab and change the view from `rose diagram` to `CPO`.
2. Enter the maximum retardation determined earlier (260 in this example) into `max R`, then press `Start CPO computation`.

{{< notice info >}}
- If the thin-section thickness is known, switch the radio button from `max R` to `thickness` and enter the value.
- When the thickness is unknown, use the mineral's maximum retardation. You can read it from the `histogram` view (`retardation`) under `information`. Here the maximum quartz value is 260.
{{< /notice >}}

{{< notice warning >}}
Histogram maxima are sensitive to outliers: a single overestimated grain can inflate the value. Check multiple representative grains or use a percentile (e.g., 95th) to refine `max R`.
{{< /notice >}}

3. After processing, a COI (crystal orientation index) entry appears in the `map` tab `image list`.

{{< notice info >}}
The `max R` value is used to recompute retardation and derive c-axis inclinations during CPO analysis.
{{< /notice >}}

<img src="{{ "/images/page/tutorial/tutorial3/pic4.png" | relURL }}" style="width: 30%;">

{{< notice warning >}}
Switching tabs or minimising the app during computation can interrupt the process. Wait until the progress bar disappears.
{{< /notice >}}

### 4.6 Inspect COI Maps

1. In `image list`, select `map coi` and choose `φ = 0–360°`. Quartz c-axis orientations now appear in pseudo-colour.

{{< notice info >}}
COI maps typically contain blank regions because tilting shifts the field of view, creating pixels without valid references.
{{< /notice >}}

<img src="{{ "/images/page/tutorial/tutorial3/pic5.png" | relURL }}" style="width: 100%;">

### 4.7 Plot Pole Figures

1. Return to `analysis`, deselect `single crystal quartz`, and leave `vein quartz` checked to focus on the vein.
2. Switch the view to `polar plot` and keep `φ = 0–360°` selected. Each grain is plotted as a single point in the pole figure.

<img src="{{ "/images/page/tutorial/tutorial3/pic6.png" | relURL }}" style="width: 100%;">

3. Enable `Plot for each pixel` to draw orientations at pixel resolution. Use this to assess intra-grain dispersion.

<img src="{{ "/images/page/tutorial/tutorial3/pic7.png" | relURL }}" style="width: 100%;">

4. Tick `display points` to overlay the sampled orientation data. NicolNavi adds 0.5% noise by default to prevent overlapping points; adjust `Point noise` if required.

<img src="{{ "/images/page/tutorial/tutorial3/pic8.png" | relURL }}" style="width: 100%;">

## 5. Wrap-Up

- CPO analysis reconstructs phase shifts across multiple videos to estimate quartz c-axis orientations.
- Correct labels let you focus on regions of interest—such as veins or single crystals—in both pole figures and COI maps.
