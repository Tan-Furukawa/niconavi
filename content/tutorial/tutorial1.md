+++
date = '2026-10-21T00:00:00+09:00'
draft = false
title = 'Tutorial 1 — Creating an angle map from one rotation video'
+++

This tutorial uses the `orikabetoge` sample, a thin section containing fossils. With only one video recorded while rotating the stage under crossed polars, you will create an **Angle map** showing c-axis orientations and a **Maximum intensity image** in which the fossil shapes are easy to see.

## 1. Download the sample video

Open the [`orikabetoge` sample data in the NicoNavi repository](https://github.com/Tan-Furukawa/niconavi/tree/main/examples/orikabetoge) and download `orikabetoge_xpl.avi`.

## 2. Load the video and enter the section thickness

Launch NicoNavi and configure the following items in the **Images** panel on the right. The numbers below correspond to the blue numbers in the image.

{{< img src="images/page/tutorial1/01-input.png" alt="Selecting the Rotated XPL video and setting thickness and white balance" >}}

1. Click **Select** for **Rotated XPL** and choose `orikabetoge_xpl.avi`, recorded while rotating the stage under crossed polars. This is the only required video; all other inputs are optional.
2. Enter the thin-section thickness, `0.04 mm`, in **Thin section thickness**. NicoNavi automatically calculates the **Maximum retardation** shown below it.
3. Enable **Gray-world white balance** if the video has not been white-balanced. The sample video has not been adjusted, so enable this option.

The **Rotated XPL + λ plate** and **XPL + λ plate (0°/45°)** inputs are not used in this tutorial. The final section explains what those additional inputs make possible.

After you select the video, its first frame appears on the left. The glowing ring-shaped features are fossils. Confirm the inputs, then click **Start** (4) to begin the calculation.

{{< img src="images/page/tutorial1/02-preview-start.png" alt="Previewing the first video frame containing fossils and clicking Start" >}}

## 3. Check the rotation center

The **Center** tab displays a concentric pattern produced by superimposing all video frames. Its center is the stage rotation center. The result is correct when the red cross lies at the center of the rings.

NicoNavi detects the center automatically. If it is offset, use the −/+ buttons for **X** and **Y**, or enter the coordinates directly. The center is already correct for this sample, so click **Continue** without changing it.

{{< img src="images/page/tutorial1/03-center.png" alt="Checking the rotation center using the concentric pattern and red cross" >}}

## 4. Interpret the Angle map

When the calculation finishes, NicoNavi moves to the **Map** tab and displays the **Angle map**.

{{< img src="images/page/tutorial1/04-angle-map.png" alt="Angle map of the fossil-bearing thin section and image-selection buttons" >}}

The Angle map combines the extinction angle with the c-axis inclination (0–90°), estimated using the thickness entered in the **Video** tab. The color chart in the upper-right corner shows the relationship between color and orientation: θ represents inclination and φ represents the extinction angle.

This view is useful for qualitative interpretation of orientation data. In this example, the colors change along the fossil shells, revealing how the orientations of the shell-forming crystals vary from place to place.

Next, inspect the following views using the buttons shown in the image:

1. **Images > Maximum intensity image**
2. **Images > extinction color** (the red button)

## 5. Check calculation quality with extinction color

**extinction color** shows the color of each pixel when it is darkest—that is, at extinction. If the rotation center and other estimates are correct, nearly the entire image appears black, as shown below.

{{< img src="images/page/tutorial1/05-extinction-color.png" alt="Successful extinction color image that appears almost entirely black" >}}

Use this view to check whether the rotation center and calculation results are reasonable. Tutorial 2 shows how unsuccessful results appear.

## 6. Observe fossils in the Maximum intensity image

**Maximum intensity image** shows each pixel at the angle where it is brightest, which is the extinction angle plus 45°. Crystals of every orientation therefore appear bright, making the fossil shapes easier to recognize.

{{< img src="images/page/tutorial1/06-maximum-intensity.png" alt="Maximum intensity image in which the fossil shapes are clearly visible" >}}

Switch between this view and **raw image > φ=0°** to see the effect more clearly.

## 7. What one video can—and cannot—determine

A single rotation video under crossed polars is sufficient to create an Angle map and a Maximum intensity image. However, extinction occurs four times during one full stage rotation, so this video alone cannot distinguish:

- whether the c-axis azimuth lies in the 0–90° or 90–180° range;
- whether the c-axis inclination lies in the 0–90° or 90–180° range—in other words, whether the c-axis points upward or downward.

To resolve these ambiguities, add the following videos or images in the **Video** tab:

- **Rotated XPL + λ plate**: a rotation video recorded with the sensitive-tint plate resolves the azimuth ambiguity.
- **XPL + λ plate (0°/45°)**: images recorded with a tilt stage resolve the inclination ambiguity.

Tutorials 2 and 3 cover analyses using these additional inputs.
