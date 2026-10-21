+++
date = '2026-10-21T00:00:00+09:00'
draft = false
title = 'Tutorial 1 — Determining c-axis orientations in a quartz thin section'
+++

This tutorial uses the `ggg3` sample dataset to walk through the complete workflow: loading videos, extracting grain boundaries, labeling mineral phases, and displaying the crystallographic preferred orientation (CPO).

## 1. Download the sample dataset

Open the [`ggg3` sample dataset in the NicoNavi repository](https://github.com/Tan-Furukawa/niconavi_app/tree/main/Examples/ggg3) and download the five videos in the folder.

## 2. Load the videos and enter the measurement settings

Launch NicoNavi and configure the following items in the **Images** panel on the right. The numbers below correspond to the blue numbers in the image.

{{< img src="images/page/tutorial/01-input-settings.png" alt="Loading videos and entering measurement settings in the Images panel" >}}

1. For **Rotated XPL**, select the video recorded while rotating the stage under crossed polars.
2. Enter the thin-section thickness in **Thin section thickness**. The sample used here is `0.022 mm` thick. The thickness does not have to be measured precisely for determining the crystallographic orientation because the normalization option described later can compensate for it.
3. For **Rotated XPL + λ plate**, select the video recorded while rotating the stage with the sensitive-tint plate inserted.
4. Enter the retardation of the sensitive-tint plate in **λ**.
5. For **0° tilted image**, select the video tilted in the 0° direction.
6. For **45° tilted image**, select the video tilted in the 45° direction.
7. For **45° reference image**, select the reference video for the 45° tilt.
8. Enable **Gray-world white balance** if white balance was not applied to the videos. The sample videos used here have not been white-balanced, so select this option.

{{< notice info >}}
The five videos used in this tutorial are included in the `ggg3` folder downloaded in Step 1.
{{< /notice >}}

After completing all inputs, click **Start** (9 in the image).

{{< img src="images/page/tutorial/02-start.png" alt="Starting the calculation after all inputs have been configured" >}}

## 3. Check the rotation center

In the **Center** tab, determine the rotation center from the concentric pattern in the image. The center is correct when the red cross is positioned at the center of the concentric rings.

NicoNavi detects the center automatically. If the result is offset, adjust the **X** and **Y** values manually. The center is already correct for this sample, so click **Continue** (10 in the image) without changing it.

{{< img src="images/page/tutorial/03-center.png" alt="Checking the concentric-ring center against the red cross in the Center tab" >}}

## 4. Check the calculation quality

Open the **Map** tab and inspect the three image-selection buttons highlighted in red. These views help you check the alignment between videos and confirm that the rotation angles were estimated correctly.

{{< img src="images/page/tutorial/04-quality-buttons.png" alt="The extinction color and original color change buttons used for quality checks" >}}

1. **extinction color** shows the color of each pixel at its darkest point. In a successful result, grain interiors are mostly black, while grain boundaries—which generally remain visible—may be brighter. Overexposure or an incorrect rotation center makes the grain interiors appear bright and noisy.
2. **original color change (0°)** is used to check the alignment between the rotation video and the 0° tilt video.
3. **original color change (45°)** is used to check the alignment between the rotation video and the 45° tilt video. It is normal for part of this image to be missing.

When the videos are misaligned, vivid red, green, and blue colors tend to appear near grain boundaries in the **original color change** views. In the comparison below, the left column shows successful results and the right column shows failed results. In the failed **extinction color** example, an incorrect rotation center makes areas other than the grain boundaries appear bright and noisy.

{{< img src="images/page/tutorial/05-quality-comparison.png" width="80%" alt="Comparison of successful and failed quality-check images" >}}

## 5. Clean the angle map and extract grain boundaries

Return to **Angle map** (1 in the image), then perform the following operations in order.

{{< img src="images/page/tutorial/06-segmentation.png" alt="Running Clean, Segment, Fill, and Apply in the Angle map view" >}}

1. Click **Clean** (2) about ten times. This operation removes image noise. Observe how the angle map becomes progressively smoother with each click.
2. Click **Segment** (3). Adjacent superpixels are merged when the angle between their c-axes is smaller than or equal to the specified value. This separates neighboring grains whose c-axis misorientation is greater than the selected angle.
3. Click **Fill** (4) until the displayed value reaches `5 px`. This operation merges thin, dark grain-boundary regions that remain extinct into the surrounding phases. A value of approximately `5 px` is a useful guideline.
4. Click **Apply** (5) to calculate the grain boundaries.

After the grain boundaries appear, check the result and click **Continue** (6).

{{< img src="images/page/tutorial/07-boundaries.png" alt="Proceeding after the extracted grain boundaries have been displayed" >}}

## 6. Label the mineral phase

For this tutorial, all grains will be treated as quartz.

1. Enter `Quartz` in the **Labels** field (1 in the image).
2. Click the **+** button (2).
3. Click anywhere in the image on the left (3).

{{< img src="images/page/tutorial/08-label-quartz.png" alt="Adding the Quartz label and clicking the image" >}}

When the entire image has been classified as quartz, click **Save** (4) and proceed to the next step.

{{< img src="images/page/tutorial/09-label-complete.png" alt="The image after all grains have been classified as Quartz" >}}

If you need to distinguish multiple minerals, add each mineral name under **Labels** and classify the corresponding phases separately.

## 7. Calculate the CPO

Open the **Analysis** tab and select **CPO** (2 in the image) from the analysis menu (1).

{{< img src="images/page/tutorial/10-analysis-cpo.png" alt="Selecting CPO in the Analysis tab" >}}

**Normalize to 90°** treats phases with retardation above the selected **Percentile** as 90° for normalization. This option can compensate when the thin-section thickness has not been measured precisely. Unless you have a specific reason to change it, leave it at the default setting.

Click **Calculate** (3) and wait for the calculation to finish.

{{< img src="images/page/tutorial/11-calculate-cpo.png" alt="Starting the CPO calculation" >}}

## 8. Display and interpret the results

After the calculation finishes, click **φ=0–360°** (4 in the image). NicoNavi displays the calculated quartz c-axis orientations as an orientation map.

{{< img src="images/page/tutorial/12-show-results.png" alt="Displaying the φ=0–360° CPO result" >}}

### Polar plots

A polar plot summarizes the distribution of c-axis orientations within the measured area. The same result can be displayed using different styles and designs.

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 2rem; align-items: start;">
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial/13-polar-plot.png" width="100%" alt="Standard polar plot of c-axis orientations" >}}
    <figcaption><strong>Standard view:</strong> Read the frequency in each orientation from the length of the bars. Directions with concentrated, longer bars contain more c-axes oriented in those directions.</figcaption>
  </figure>
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial/14-polar-plot-styled.png" width="100%" alt="Alternative design for the c-axis polar plot" >}}
    <figcaption><strong>Alternative design:</strong> This is another presentation of the same orientation data. Choose the style that makes the result easiest to compare and interpret.</figcaption>
  </figure>
</div>

### Orientation maps

An orientation map uses color to show the direction of the c-axis in each grain across the thin section.

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 2rem; align-items: start;">
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial/15-map-0-360.png" width="100%" alt="φ=0–360° orientation map incorporating tilt information" >}}
    <figcaption><strong>φ=0–360°:</strong> This result incorporates information from the tilt videos and represents c-axis directions over the full 360° range.</figcaption>
  </figure>
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial/16-map-0-180.png" width="100%" alt="φ=0–180° orientation map without tilt information" >}}
    <figcaption><strong>φ=0–180°:</strong> This result is calculated without using the tilt videos. Because estimating tilt information is difficult, the φ=0–360° map on the left appears more finely mixed and slightly more scattered than this map.</figcaption>
  </figure>
</div>
