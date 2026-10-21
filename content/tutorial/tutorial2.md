+++
date = '2026-10-21T00:00:00+09:00'
draft = false
title = 'Tutorial 2 — Classifying mineral phases and analyzing SPO and CPO'
+++

This tutorial uses the `ym3-2` rotation videos to extract grain boundaries, classify grains as quartz, mica, or other minerals, analyze shape preferred orientation (SPO), and calculate the crystallographic preferred orientation (CPO) of quartz c-axes. Even without tilt images, c-axis orientations can be determined over the φ=0–180° range.

## 1. Load the videos and enter the measurement settings

Launch NicoNavi and configure the videos and measurement settings in the **Images** panel on the right. The numbers below correspond to the blue numbers in the image.

{{< img src="images/page/tutorial2/01-input.png" alt="Loading rotation videos and entering measurement settings in the Images panel" >}}

1. Click **Select** for **Rotated XPL** and choose `ym3-2_xpl.avi`, which was recorded while rotating the stage under crossed polars. This video is required.
2. Enter the thin-section thickness, `0.03 mm`, in **Thin section thickness**. The value does not have to be exact because **Normalize to 90°** can compensate for thickness errors during the CPO calculation.
3. Click **Select** for **Rotated XPL + λ plate** and choose `ym3-2_lambda.avi`, which was recorded while rotating the stage with the sensitive-tint plate inserted.
4. Enter the sensitive-tint plate retardation, `530 nm`, in **λ**.
5. These videos have not been white-balanced, so enable **Gray-world white balance**.

The **0° tilted image**, **45° tilted image**, and **45° reference image** inputs are optional and are not used in this tutorial. The analysis can still be completed, but the up/down direction of the c-axis—that is, φ=0–360°—cannot be determined.

After you select a video, its first frame appears on the left. Use **xpl** and **xpl+λ** under **Images** to switch between the two videos. Confirm the inputs, then click **Start** (6 in the image).

{{< img src="images/page/tutorial2/02-video-preview.png" alt="Previewing a loaded video frame and clicking Start" >}}

## 2. Check the rotation center

In the **Center** tab, verify that the red cross lies at the center of the concentric pattern. If it is offset, use the −/+ buttons for **X** and **Y** to correct it. The center is already correct for this sample, so click **Continue** (7) without changing it.

{{< img src="images/page/tutorial2/03-center.png" alt="Checking the concentric pattern against the red cross in the Center tab" >}}

## 3. Check calculation quality with the extinction image

Open the **Map** tab and click the red **extinction color** button under **Images** (1). This image shows the color of every pixel at its darkest point and helps verify the image registration and rotation-angle estimation.

{{< img src="images/page/tutorial2/04-extinction-check.png" alt="Displaying extinction color in the Map tab" >}}

In a successful result, grain interiors are mostly black. Grain boundaries generally do not become completely black and remain as the main visible features. Overexposure or an incorrect rotation center causes grain interiors to remain bright and appear noisy.

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(210px, 1fr)); gap: 1.5rem; align-items: start;">
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial2/quality-correct.png" width="100%" alt="Successful extinction image with the correct center and exposure" >}}
    <figcaption><strong>Successful:</strong> Grain interiors are dark and mainly the boundaries remain visible.</figcaption>
  </figure>
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial2/quality-overexposed.png" width="100%" alt="Failed extinction image caused by overexposure" >}}
    <figcaption><strong>Overexposed:</strong> Bright areas remain within the grains.</figcaption>
  </figure>
  <figure style="margin: 0;">
    {{< img src="images/page/tutorial2/quality-center-shifted.png" width="100%" alt="Failed extinction image caused by a shifted rotation center" >}}
    <figcaption><strong>Center shifted:</strong> Areas away from boundaries appear bright and noisy.</figcaption>
  </figure>
</div>

## 4. Clean the angle map and extract grain boundaries

Return to **Angle map** (1 in the image), then perform the following operations in order.

{{< img src="images/page/tutorial2/05-angle-clean.png" alt="Running Clean, Segment, Fill, and Apply in the Angle map view" >}}

1. Click **Clean** (2) about ten times. It removes image noise; observe the angle map becoming progressively smoother.
2. Click **Segment** (3). Adjacent superpixels are merged when the angle between their c-axes is less than or equal to the selected value. This separates neighboring grains whose c-axis misorientation is greater than the selected angle.
3. Click **Fill** (4) until the displayed value reaches `5 px`. It merges thin, dark boundary regions that remain extinct into the surrounding phases when they are no wider than the selected value. About `5 px` is a useful guideline.
4. Click **Apply** (5) to calculate the grain boundaries.

Once **grain map > grains** displays each grain in a different color, inspect the result and click **Continue** (7).

{{< img src="images/page/tutorial2/06-grains.png" alt="Color-coded grain map and the Continue button" >}}

## 5. Classify quartz, mica, and other grains

In this tutorial, grains are classified into three phases: **Quartz**, **Mica**, and **Other**.

1. Enter a mineral name in **Label name** (1).
2. Click **+** (2) to add the label. Repeat this for `Quartz`, `Mica`, and `Other`. Label names are arbitrary, but these three names are used below.

{{< img src="images/page/tutorial2/07-labels-add.png" alt="Adding mineral labels in the Filter tab" >}}

Select the radio button for the label you want to classify (3), then click grains belonging to that mineral in the image on the left (4). For mica, look for elongated grains with vivid interference colors. You do not need to click every grain; selecting several representative examples is enough.

{{< img src="images/page/tutorial2/08-label-mica.png" alt="Selecting the Mica label and clicking representative mica grains" >}}

Selected training grains are outlined in red. When Mica is the only class with training examples, all grains are initially predicted as Mica and displayed in green.

{{< img src="images/page/tutorial2/09-label-mica-only.png" alt="Intermediate classification with training examples for Mica only" >}}

Add representative grains for Quartz and Other in the same way. NicoNavi automatically classifies the remaining grains from the examples: quartz is blue, mica is green, and other grains are orange. If a grain is misclassified, select the correct label and click that grain to add another training example.

Use **Opacity** (5) to control the strength of the color overlay. Move it right for stronger colors or left to see the underlying thin-section image more clearly. Expand **Learning features** with **+** to choose the features used for classification, including color, elongation, size, and position. For example, enable **Color** when a mineral has a distinctive color. This tutorial uses the defaults.

{{< img src="images/page/tutorial2/10-label-classified.png" alt="Grains classified as Quartz, Mica, and Other" >}}

When the classification looks correct, click **Save** (6). **Result** shows the number of training examples and classified grains; 75 training examples were entered in this example. If **Save** is not visible, scroll down in the right-hand panel.

{{< img src="images/page/tutorial2/11-label-save.png" alt="Saving the completed phase classification" >}}

## 6. Compare SPO and azimuth with rose diagrams

Open the **Analysis** tab and choose **rose diagram** from the first drop-down menu (1).

{{< img src="images/page/tutorial2/12-analysis-type.png" alt="Selecting rose diagram in the Analysis tab" >}}

Choose **shape preferred orientation** from the second drop-down menu (2) to display a rose diagram of the grain long-axis orientations (SPO). Clear the **Mica** and **Other** checkboxes (3 and 4) to show only the quartz SPO.

**Information** displays the mean orientation and circular variance. A circular variance closer to zero indicates more closely aligned grains. **Flip** reverses the rose diagram direction, **Opacity** changes bar transparency, and **Bins** changes the number of bars. These options affect only the display, not the calculated result.

{{< img src="images/page/tutorial2/13-spo-quartz.png" alt="SPO rose diagram for quartz only" >}}

Select only Mica to compare preferred orientation between phases. In this example, mica has a circular variance of `0.228`, compared with `0.620` for quartz, so the mica grains are more closely aligned.

{{< img src="images/page/tutorial2/14-spo-mica.png" alt="SPO rose diagram for mica only" >}}

Choose **azimuth** in the second drop-down menu (5) to display a rose diagram of c-axis azimuths. Under **Grain value**, choose whether each grain is represented by its median or mean value.

{{< img src="images/page/tutorial2/15-azimuth.png" alt="Rose diagram of c-axis azimuths" >}}

## 7. Inspect grain shapes and phase distributions on maps

Choose **SPO** from the first drop-down menu (6) to display a map in which color represents the grain long-axis orientation. Select Mica and Other as well (7 and 8), then click **Images > ellipse** (9).

{{< img src="images/page/tutorial2/16-spo-map.png" alt="Selecting all phases and displaying ellipses on the SPO map" >}}

Each grain is approximated by an ellipse, colored by phase: quartz is blue, mica is green, and other grains are orange. Select **ellipse (major axis)** to show only the long axis of each ellipse.

{{< img src="images/page/tutorial2/17-ellipses-all.png" alt="Ellipse approximations for grains in all phases" >}}

Clear the Mica and Other checkboxes (10 and 11) to show only the quartz ellipses, then move to the **Map** tab (12).

{{< img src="images/page/tutorial2/18-ellipses-quartz.png" alt="Showing quartz ellipses only and moving to the Map tab" >}}

Click **Images > Maximum intensity image** (13). This view displays the color of each pixel at the angle where it is brightest—the extinction angle plus 45°. Because Mica and Other are cleared, those phases appear black and only quartz is displayed. Phase visibility is synchronized across all tabs.

{{< img src="images/page/tutorial2/19-max-intensity.png" alt="Maximum intensity image displaying quartz only" >}}

## 8. Calculate the quartz CPO

Return to the **Analysis** tab and choose **CPO** from the first drop-down menu (14). The displayed refractive indices (ω and ε) are for quartz, so leave them unchanged for this analysis.

**Normalize to 90°** normalizes phases whose retardation is above the selected **Percentile** by treating them as 90°. This can compensate for thin-section thickness errors. Unless you have a specific reason to change it, leave the default setting. Click **Calculate** (15) and wait for the calculation to finish.

{{< img src="images/page/tutorial2/20-cpo-settings.png" alt="Checking CPO settings and clicking Calculate" >}}

After calculation, click **map coi > φ=0–180°** (16). The orientation map uses color to show c-axis directions; the color wheel in the upper-right corner gives the color-to-orientation key.

The “CPO computed, but ...” message under **Information** appears because no tilt images were supplied. A φ=0–360° result is therefore unavailable, but φ=0–180° can still be calculated from the rotation video recorded with the sensitive-tint plate.

Next, click **polar plot > φ=0–180°** (17).

{{< img src="images/page/tutorial2/21-cpo-map.png" alt="C-axis orientation map for φ=0–180 degrees calculated without tilt images" >}}

The polar plot shows the density distribution of c-axis orientations. Use **Group by** to aggregate the result by grain or by pixel. The lower half of the plot is empty because tilt images—which are needed to distinguish the up/down direction of the c-axis—were not used.

{{< img src="images/page/tutorial2/22-polar-plot.png" alt="Polar plot of c-axis orientations calculated without tilt images" >}}

## 9. Save the project and export results

Use the menu (≡) in the upper-right corner to save the project or export results.

{{< img src="images/page/tutorial2/23-export-menu.png" width="35%" alt="Save and export menu" >}}

- **Save project** saves the input files, settings, and calculated results as a project file.
- **Load project** opens a saved project.
- **Export image (PDF)** exports the image currently displayed on the left as a PDF.
- **Export grain data** exports a table of the calculated values for each grain.
