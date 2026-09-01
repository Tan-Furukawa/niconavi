+++
date = '2026-08-31T00:00:00+09:00'
draft = false
title = 'Tutorial 1 - CPO Analysis with the GGG3 Dataset'
+++

## 1. Overview

This tutorial runs a CPO (Crystallographic Preferred Orientation) analysis on the GGG3 orthoquartzite dataset. You will load five optical videos, work through the `video` / `center` / `map` / `filter` / `analysis` tabs, and inspect quartz c-axis orientations on a polar plot.

In each figure below, the **yellow numbers** mark the controls to use, in the order they are used on that tab.

## 2. Video Set

| NicoNavi input | File |
| --- | --- |
| `XPL Rotated` | `ggg3_xpl.avi` |
| `XPL + λ-Plate Rotated` | `ggg3_lambda.avi` |
| `0° tilt` | `ggg3_tilt_0.avi` |
| `45° tilt` | `ggg3_tilt_45.avi` |
| `45° not tilt` | `ggg3_horiz.avi` |

## 3. Workflow

### 3.1 `video` Tab: Load the Videos

{{< img src="images/page/tutorial/tutorial1/pic1.png" alt="video tab" >}}

The yellow numbers correspond to the following steps.

| No. | Control | Action |
| --- | --- | --- |
| **1** | `XPL Rotated` | Click `Select` and choose `ggg3_xpl.avi`. |
| **2** | `XPL + λ-Plate Rotated` | Choose `ggg3_lambda.avi`. |
| **3** | `0°` row of `XPL + λ-Plate 0°/45°` | Choose `ggg3_tilt_0.avi`. |
| **4** | `45°` row (tilt) | Choose `ggg3_tilt_45.avi`. |
| **5** | `45°` row (horiz) | Choose `ggg3_horiz.avi`. |
| **6** | `thin section thickness` | The thin-section thickness. Enter `0.022` mm. |
| **7** | `λ` | The retardation plate value. Keep `530.0` nm unless the data were acquired with a different plate. |
| **8** | `gray-world white balance` | Check this when the illumination colour cast was not corrected during acquisition. Check it for this dataset. |
| **9** | `▶ start` | Starts preprocessing. NicoNavi switches to the `center` tab when loading finishes. |

### 3.2 `center` Tab: Confirm the Rotation Centre

{{< img src="images/page/tutorial/tutorial1/pic2.png" alt="center tab" >}}

1. The left image stacks the frame-to-frame change over the whole video, so stage rotation appears as a concentric pattern.
2. Confirm that the red cross sits at the centre of that pattern. Here `cx = 490` and `cy = 266` are already centred, so continue as is.
3. If it is off-centre, adjust `cx` and `cy` with the `−` / `+` buttons.
4. Click `▶ continue` to build the angle and colour maps.

### 3.3 `map` Tab: Inspect the Maps and Segment Grains

{{< img src="images/page/tutorial/tutorial1/pic3.png" alt="map tab" >}}

On the `map` tab, first check the results in the image list on the left (numbers 1–3), then segment grains in the right-hand panel (numbers 4–9).

| No. | Control | Action |
| --- | --- | --- |
| **1** | `extinction color` in the `extinction` group (red button) | The colour image at extinction. Red marks an important image that has not been opened since the last recalculation. Click it to check the content. |
| **2** | `original color change (0°)` in the `xpl + λ` group (red button) | How much the colour changed from the original image in the 0° tilted view. A visible change means the tilted images were registered correctly. |
| **3** | `original color change (45°)` (red button) | The same check for the 45° tilted view. A nearly black result suggests the tilted field of view does not match. |

Once numbers 1–3 look right, segment the angle map into grains in the right-hand panel. Colours in the angle map represent optical orientation, so grouping pixels of similar colour builds the grain regions. Work through numbers 4–9 in order: remove noise (`Clean`) → segment (`Segmentation`) → fill the gaps left by segmentation (`Fill boundary`) → register the result (`OK`).

| No. | Control | Action |
| --- | --- | --- |
| **4** | `Clean` | Reduces isolated noisy pixels in the angle map. The counter increases on each click, so click it **10 times**. |
| **5** | `angle:` | The angle difference treated as the same grain. Keep the default, `5`. |
| **6** | `Segmentation` | Groups regions of similar angle into grains. Click it after setting numbers 4 and 5. |
| **7** | `Fill boundary` | Fills the thin dark lines left after segmentation. The first click sets `2.0 px` and each later click adds `0.5 px`, so `5.0 px` takes **seven clicks** in total. |
| **8** | `OK` | Registers the result as the grain boundary map. |
| **9** | `▶ Continue` | Moves to the `filter` tab. |

The fan-shaped colour chart at the top right maps combinations of extinction angle θ and retardation φ to colour. The large image on the left is the `Angle map`, where a single colour region corresponds to one grain of uniform optical orientation.

Use the buttons in the image list to check the processing.

| Map | What to check |
| --- | --- |
| `Angle map` | Similar colours should follow coherent optical-orientation domains. |
| `color` | The quartz interference colours should be continuous, without large saturated regions. |
| `extinction angle (φex)` | Extinction-angle boundaries should roughly match the visible quartz grain structure. |
| `azimuth` | The 0–180° azimuth should be resolved where the λ-plate video is valid. |
| `raw image` (φ=0°/22.5°/45°/67.5°) | The source frame at each rotation angle. Check for blur and focus. |
| `xpl + λ` tilt images | The tilted views should not be shifted too far from the original field. |

The `output` panel at the bottom shows the processing log. `Image processing completed.` means preprocessing has finished.

The figure below shows the state **right after steps 4–8**. Confirm that `Clean` is `10`, `angle` is `5`, and `Fill boundary` is `5.0 px`, then click `▶ Continue`.

{{< img src="images/page/tutorial/tutorial1/pic4.png" alt="map tab before Continue" width="45%" >}}

### 3.4 `filter` Tab: Label the Quartz Regions

{{< img src="images/page/tutorial/tutorial1/pic5.png" alt="filter tab" >}}

The `filter` tab assigns mineral labels to grains. The white lines are the grain boundaries registered on the `map` tab.

| No. | Control | Action |
| --- | --- | --- |
| **1** | `+` button next to `Labels` | Registers the label name you typed (click it after entering number 2). |
| **2** | `Label name` field | Type the label name. Use `Quartz` here. |
| **3** | A grain in the image | With the label selected, click any quartz grain. The clicked grain becomes training data. |
| **4** | `Done` | Confirms the classification and moves to the `analysis` tab. |

Use `Boundaries` (show grain boundaries), `Training boxes` (show training data), and the `Opacity` slider (overlay strength) in the `Display` panel to check the prediction against the training data. `Labeled samples` and `Predicted class distribution` in the `Result` panel update as you work.

The figure below shows the state **after clicking in step 3**.

{{< img src="images/page/tutorial/tutorial1/pic6.png" alt="filter tab after labelling" >}}

### 3.5 `analysis` Tab: Run the CPO Calculation

{{< img src="images/page/tutorial/tutorial1/pic7.png" alt="analysis tab, CPO selected" width="45%" >}}

| No. | Control | Action |
| --- | --- | --- |
| **1** | Plot type dropdown | Change it from `rose diagram` (the default) to **`CPO`**. |

Also confirm that `Quartz` is checked at the top. Uncheck any non-quartz label before running the CPO calculation.

Selecting `CPO` changes the parameter panel as shown below. Keep every default and click `calculate`.

{{< img src="images/page/tutorial/tutorial1/pic8.png" alt="CPO parameters" width="45%" >}}

| Item | Value | Meaning |
| --- | --- | --- |
| `ω` / `ε` | `1.544` / `1.553` | The ordinary and extraordinary refractive indices of quartz. Keep the defaults when analysing quartz. |
| `90° normalize` | on | Rescales the inclination using the retardation distribution. Leave it on for a first pass. |
| `percentile` | `95.0` % | The percentile used for that correction. Keep the default. |
| `calculate` | — | Starts the CPO calculation. Wait until the progress bar disappears. |

### 3.6 Review the CPO Result

{{< img src="images/page/tutorial/tutorial1/pic9.png" alt="CPO result" >}}

When the calculation finishes, the quartz c-axis polar plot (lower-hemisphere projection) appears on the left.

- **Polar plot**: colour shows the density of c-axis orientations (`density`, the colour bar on the right). This sample has a moderate concentration towards the northwest and north. `N` / `S` / `E` / `W` are directions on the thin section.
- **`Information` panel**: a summary of the calculation.
  - `Orientation: addition image + E-down tilt` — the image combination used to resolve the tilt direction.
  - `Grain samples: 304` — the number of grains used in the plot.
  - `90 deg normalize: on` / `Theta(P95) -> 90 deg: 56.00 deg` — the applied correction.
  - `Predicted thickness: 0.01508 mm` — the effective thickness back-calculated from retardation.
  - `Color fit y = alpha * M @ predicted + b` — the fit between theoretical and measured colours.

Switch between the following in the image list on the left.

| Group | Buttons | Content |
| --- | --- | --- |
| `map` | `extinction angle (Φ)`, `azimuth (0°-180°)`, `inclination`, `inclination (0°-180°)` | Extinction angle, azimuth, and inclination maps. |
| `map coi` | `φ=0°-90°`, `φ=0°-180°`, `φ=0°-360°` | COI maps showing c-axis orientation in pseudo-colour. Start with `φ=0°-360°`. |
| `polar plot` | `φ=0°-90°`, `φ=0°-180°`, `φ=0°-360°` | Polar plots. The figure above has `φ=0°-360°` selected. |
| `color check` | `RGB before correction`, `RGB after correction` | Theoretical versus measured λ-plate colours. A better post-correction trend means the colour model matches the measurement. |

The `Grain boundaries` checkbox at the top right toggles the grain boundary overlay on the maps.

{{< notice info >}}
Blank regions in COI maps are expected where the tilted and horizontal fields of view do not overlap.
{{< /notice >}}

### 3.7 Save the Results

1. Choose `Save project` from the top-right menu (≡) to store the `.niconavi` project.
2. Use `Save image as PDF` to export the currently displayed map or plot.
3. Use `Save grain information as CSV` for grain-level measurements.

## 4. Wrap-Up

- On the `video` tab, load the five videos and the thin-section thickness, then start preprocessing (figure 1, numbers 1–9).
- Grains are extracted on the `map` tab with `Clean` → `Segmentation` → `Fill boundary` → `OK` (figure 3, numbers 4–9).
- Labelling happens on the `filter` tab: add a label → click a grain → `Done` (figure 5, numbers 1–4).
- Verify the CPO result on both the COI map and the polar plot before exporting figures.
