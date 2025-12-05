+++
date = '2025-10-15T13:10:14+09:00'
draft = false
title = 'Tutorial 2 - Mineral Extraction and Visualisation'
+++

## 1. Overview

This tutorial uses a sector-zoned garnet video to demonstrate mineral-specific boundary extraction and how to highlight optical anisotropy. Building on Tutorial 1, you will tweak settings to emphasise extinction within a single crystal and practise assigning mineral labels.

## 2. Prerequisites

- NicolNavi is running with the relevant project open.
- You can access `nicolnavi_app/Examples/sector_zoning.avi`.
- You have completed Tutorial 1 (preprocessing, boundary detection, labelling).

## 3. Workflow

### 3.1 Load the Video

1. Click `Select` on the right panel.
2. Choose `nicolnavi_app/Examples/sector_zoning.avi` and open it.
3. The left panel shows the first frame as a 1000 px square image.
4. Press `Start` to begin discretisation and rotation-centre estimation.

### 3.2 Adjust the Rotation Centre

1. After processing, the rotation-centre screen appears.

<img src="{{ "/images/page/tutorial/tutorial2/pic1.png" | relURL }}" style="width: 100%;">

2. In this dataset the detected centre is offset from the true concentric pattern. Click `cx` and `cy` to move the red cross to the actual centre.

<img src="{{ "/images/page/tutorial/tutorial2/pic2.png" | relURL }}" style="width: 100%;">
Figure: Centre after manual adjustment.

3. Click `Continue` to confirm.

### 3.3 Review Maps and Brightness Correction

1. Open `Image list` and examine the standard maps.

| Map | Description |
| --- | --- |
| `color` | Brightest colours observed during a rotation. |
| `extinction color` | Colours at the darkest instant. Re-run preprocessing if full extinction is missing. |
| `R` | Retardation at each pixel within the specified search range. |
| `extinction angle` | Extinction angles for each pixel. |
| `raw image` | Original frames. Selecting `phi = 22.5°` shows the frame at that angle. |

2. Switching between `color` and `extinction color` may reveal that `color` looks darker.

<img src="{{ "/images/page/tutorial/tutorial2/pic3.png" | relURL }}" style="width: 80%;">
`Image list = color`

<img src="{{ "/images/page/tutorial/tutorial2/pic4.png" | relURL }}" style="width: 80%;">
`Image list = extinction color`

3. By default, `color` applies **brightness correction**. If \(B_{\max}(x, y)\) and \(B_{\min}(x, y)\) are the maximum and minimum brightness within a rotation, the display intensity is

   \[
   I_{\text{corr}}(x, y) = B_{\max}(x, y) - B_{\min}(x, y).
   \]

   The correction compensates for uneven illumination. When the sensor saturates, however, \(B_{\max}(x, y) \approx B_{\min}(x, y)\), making the corrected image look too dark.

4. If saturation is suspected, clear the **brightness correction** checkbox. NicolNavi then shows \(I_{\text{corr}}(x, y) = B_{\max}(x, y)\) directly so you can inspect the true brightness.

<img src="{{ "/images/page/tutorial/tutorial2/pic5.png" | relURL }}" style="width: 80%;">
`Image list = color` with brightness correction disabled.

### 3.4 Detect Grain Boundaries

1. Once the brightness setting is confirmed, click `Detect Grain Boundary` to generate the initial boundary overlay.
2. Adjust `median filter` and `parameters` if needed. In this example `boundary connectivity` is set to 5.
3. Press `Calculate grain boundaries` to apply the adjustments.
4. When the boundaries look correct, choose `Continue` to move to the labelling screen.

<img src="{{ "/images/page/tutorial/tutorial2/pic6.png" | relURL }}" style="width: 30%;">

### 3.5 Assign Mineral Labels

1. Enter `garnet` in `Label Name` and press `+`. Add `inclusion` and `matrix` in the same way.
2. Select `garnet` and click 5–10 representative grains in the left panel to add training samples.
3. Repeat for `inclusion` and `matrix`.
4. If misclassification persists, expand each training set until the preview stabilises. In this dataset 48 grains were labelled.
5. Click `Done` to confirm.

<img src="{{ "/images/page/tutorial/tutorial2/pic7.png" | relURL }}" style="width: 100%;">

### 3.6 Visualise Optical Anisotropy

1. Switch to the `Analysis` tab and uncheck `inclusion` and `matrix` so only garnet remains.

<img src="{{ "/images/page/tutorial/tutorial2/pic8.png" | relURL }}" style="width: 30%;">

2. Return to the `map` tab and set `image list` to `extinction angle`. All other minerals render in black, highlighting the sector zoning within the garnet.

<img src="{{ "/images/page/tutorial/tutorial2/pic9.png" | relURL }}" style="width: 100%;">

3. Use the top menu `Save as PDF` to export the view if required.

{{< notice info >}}
This approach also emphasises undulose extinction in single crystals.
{{< /notice >}}

## 4. Wrap-Up

- Disable **brightness correction** when saturation darkens the `color` map.
- Accurate mineral labels let you isolate maps such as `extinction angle` for each mineral, making it easy to crop and visualise the desired phase.
