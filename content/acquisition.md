+++
date = '2025-10-15T13:10:14+09:00'
draft = false
title = 'Data Acquisition'
+++

This page outlines how to capture microscope videos that NicolNavi can process. Start with the pre-shoot checklist, then choose the workflow that matches your goal: capturing a rotating-stage video or collecting the datasets required for quartz c-axis orientation analysis.

## Preparation Before Filming

Confirm the following before you begin.

- You can record and save microscope videos on the system in use.
- The microscope stage has angle markings for rotation.
- When the stage is set to 0°, the line that joins 0° and 180° is parallel to the camera sensor.

<img src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic1.svg" style="width: 70%;">
Figure: Align the stage with the sensor. Place paper on the stage and adjust the camera until the image appears level on the monitor.

- The lower Nicol vibrates along the east–west direction and the upper Nicol along the north–south direction.

## Workflow 1: Capture a Rotation Video (Baseline Texture Analysis)

Use this workflow to shoot a standard stage-rotation video. It supports boundary detection and general texture work.

### Steps

1. Set the optical system to crossed Nicols.
2. Rotate the stage to 0° (diagram a below).
3. Place the thin section so that its long axis is parallel to the 0°–180° line (diagram b).
4. Start recording.
5. Rotate the stage slowly and counterclockwise for a full 360° (diagram c). About one minute per revolution keeps the motion stable. Minor pauses or speed changes are acceptable.
6. Stop recording and save the file as `.avi` or `.mp4`.

<img src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic2.svg" style="width: 70%;">
Figure: Rotate the stage smoothly from 0° to 360°.

<video controls width="70%">
    <source src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic3.mp4" type="video/mp4">
</video>
Figure: Sample rotation video. Aim for roughly one minute per revolution at a steady pace.

## Workflow 2: Quartz c-Axis Orientation Analysis

This workflow compares a tilted thin section with a horizontal one to quantify quartz orientations. The method works even without a universal stage and includes an example of a simple tilting jig. A tilt angle of roughly 10° is sufficient; high precision is not required.

{{< notice warning >}}
The c-axis orientation is derived from subtle colour changes. Illumination, sensor response, and sample conditions can all introduce misclassification. In particular, camera white balance strongly affects retardation readings: retardations of 0–300 nm should appear grey to pale yellow, but some systems add red or blue tints. Use the retardation chart below and adjust white balance so that the low-retardation reference matches expectations.

<img src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic12.png" style="width: 100%;">

Always cross-check your results against samples with known orientations (for example, EBSD data). Record the capture and lighting conditions so that the measurement can be reproduced.
{{< /notice >}}

### 2-1. Build a Tilting Jig

Prepare a support that lets you tilt the thin section without slipping. One example is shown below.

<img src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic6.svg" style="width: 70%;">

**Materials**
- Thin section measuring 50 mm × 30 mm (thickness ≤ 0.03 mm)
- Weights totalling a few dozen grams
- A smooth board about 3.5–4.5 mm thick (overall size can be a few centimetres)
- Double-sided tape cut into strips about 1 mm wide

**Assembly**

1. Stick a strip of double-sided tape to the edge of the board and remove the backing.

   <img src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic4.svg" style="width: 70%;">


   {{< notice example >}}
   The author stacks three new thin sections, tapes them together, and applies the narrow tape on top. That combination stabilises the pivot height and grip so the section stays in place.

   <img src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic5.jpg" style="width: 70%;">
   {{< /notice >}}

3. Place the thin section so that the area of interest sits close to the hinge (the tape) without touching the board.

   <img src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic7.svg" style="width: 70%;">

{{< notice example >}}
The photo shows the tilted thin section on the microscope stage. A weight keeps the angle fixed; here a hex wrench is used.

   <img src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic10.jpg" style="width: 70%;">

   Figure: Tilted setup

   <img src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic11.jpg" style="width: 70%;">

   Figure: Horizontal setup with the weight applied
{{< /notice >}}

### 2-2. Capture Sequence

Record the following five videos in order. Rename each file immediately after recording.

<img src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic8.svg" style="width: 100%;">

Figure: Capture flow. Record videos a through e.

#### Video 1: With Compensator, Tilted Section, Stage at 0°

1. Switch to crossed Nicols and insert the first-order red (λ) plate.
2. Set the stage to 0° and align the thin section with the 0°–180° line.
3. Tilt the section and focus on the **left edge** in the monitor view.

{{< notice warning >}}
Polarising microscopes invert the image horizontally, so focusing on the left edge in the monitor corresponds to the right edge on the stage.
{{< /notice >}}

4. Start recording and move the focus away from the objective over about 10 seconds until the monitor shows the right edge in focus (diagram a). Stop the recording.

<video controls width="70%">
    <source src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic9-0deg-tilt.mp4" type="video/mp4">
</video>

#### Video 2: With Compensator, Tilted Section, Stage at 45°

1. Rotate the stage to 45° and focus on the bottom-left edge in the monitor view.

{{< notice warning >}}
Because the image is inverted, this corresponds to the top-right edge on the stage.
{{< /notice >}}

2. Start recording and move focus away from the objective for roughly 10 seconds. Stop when the monitor shows the top-right edge in focus (diagram b).

<video controls width="70%">
    <source src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic9-45deg-tilt.mp4" type="video/mp4">
</video>

#### Video 3: With Compensator, Horizontal Section, Stage at 45°

1. Add the weight to level the section and focus on the area of interest (diagram c).
2. Start recording and stop immediately. A one-second clip is sufficient.

{{< notice note >}}
This clip is used as reference data for the `extinction color` map. As long as you can pair it with the tilted videos, the exact length is unimportant.
{{< /notice >}}

<video controls width="70%">
    <source src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic9-45deg-not-tilt.mp4" type="video/mp4">
</video>

#### Video 4: With Compensator, Horizontal Section, Stage Rotation

1. Return the stage to 0°.
2. Start recording and, with the weight in place, rotate the stage counterclockwise through 360° (diagram d). About one minute per cycle works well.
3. Stop recording.

<video controls width="70%">
    <source src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic9-xpl-lambda.mp4" type="video/mp4">
</video>

#### Video 5: Without Compensator, Horizontal Section, Stage Rotation

1. Remove the λ plate.
2. Start recording and rotate the stage counterclockwise through 360° (diagram e) using the same speed as Video 4.
3. Stop recording.

<video controls width="70%">
    <source src="https://tan-furukawa.github.io/niconavi/images/page/acquisition/pic9-xpl.mp4" type="video/mp4">
</video>

Save each file with a clear name as soon as the capture ends.
