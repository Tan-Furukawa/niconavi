+++
date = '2025-10-15T13:10:14+09:00'
draft = false
title = 'Data Acquisition'
+++

This page outlines how to capture microscope videos that NicolNavi can process. Start with the pre-shoot checklist, then choose the workflow that matches your goal: capturing a rotating-stage video or collecting the datasets required for quartz c-axis orientation analysis.

## Preparation Before Filming

Before recording, confirm that the microscope stage has angle markings for rotation. Set the stage to 0°, then adjust the camera so that the line joining 0° and 180° is parallel to the camera sensor.

{{< img src="images/page/acquisition/pic1.svg" width="70%" >}}
Figure: Align the stage with the sensor. Place paper on the stage and adjust the camera until the image appears level on the monitor.

Also confirm that the lower Nicol vibrates along the east–west direction and the upper Nicol along the north–south direction.

## Coordinate System and Orientation Definitions

The procedures below use the microscope and monitor/video coordinate systems shown here. Before recording, confirm that the directions and stage rotation match the diagrams.

{{< img src="images/page/acquisition/coordinate-microscope.png" width="80%" alt="Microscope coordinate system and polarizer/analyzer arrangements" >}}

Figure: Microscope coordinate system and direction of stage rotation.

- **Microscope setup (a, b):** Panels (a) and (b) show the polarizer and analyzer vibration directions interchanged. Either arrangement produces the same result, so use the one that matches your microscope. Also check the slow and fast axes of the λ plate (sensitive-tint plate), and rotate the stage in the direction shown by the arrow.

{{< img src="images/page/acquisition/coordinate-monitor.png" width="80%" alt="Monitor and video coordinate system with angular definitions" >}}

Figure: Monitor/video coordinate system and the definitions of azimuth and inclination.

- **Monitor/video coordinates (a):** In both the monitor view and the recorded video, confirm that S is at the top, N at the bottom, E at the left, and W at the right. This is the uncorrected camera view, with no image flipping or rotation applied, so the microscope-stage directions appear reversed. NicolNavi expects videos recorded in this orientation.
- **Angle definitions (b):** `φ` is the c-axis azimuth and `θ` is the c-axis inclination. For `θ < 90°` and `θ > 90°`, the c-axis points in opposite directions.

## Workflow 1: Capture a Rotation Video (Baseline Texture Analysis)

Use this workflow to shoot a standard stage-rotation video. It supports boundary detection and general texture work.

### Steps

1. Set the optical system to crossed Nicols.
2. Rotate the stage to 0° (diagram a below).
3. Place the thin section so that its long axis is parallel to the 0°–180° line (diagram b).
4. Start recording.
5. Rotate the stage slowly and counterclockwise for a full 360° (diagram c). About one minute per revolution keeps the motion stable. Minor pauses or speed changes are acceptable.
6. Stop recording and save the file as `.avi` or `.mp4`.

{{< img src="images/page/acquisition/pic2.svg" width="70%" >}}
Figure: Rotate the stage smoothly from 0° to 360°.

<video controls width="70%">
    <source src="{{< url "images/page/acquisition/pic3.mp4" >}}" type="video/mp4">
</video>
Figure: Sample rotation video. Aim for roughly one minute per revolution at a steady pace.

## Workflow 2: Quartz c-Axis Orientation Analysis

### 2-1. Prepare a Tilting Jig

| | Option | Notes |
| --- | --- | --- |
| **A** | 3D-print the dedicated tilt stage | The tilt axis sets the angle, so switching between tilted and horizontal is repeatable. |
| **B** | Build one from a board and double-sided tape | No 3D printer needed. The angle is held by a weight. |

#### A. If you have a 3D printer

The STL files and assembly instructions for the dedicated tilt stage are published here:

- [Tan-Furukawa/niconavi-tilt-stage](https://github.com/Tan-Furukawa/niconavi-tilt-stage)

{{< img src="images/page/acquisition/pic13.jpg" width="70%" >}}

Figure: The assembled tilt stage. Clips hold the thin section, which is observed through the window at the centre of the main plate.

Print four kinds of parts — frame, main plate, bearings, and clips — and assemble them with six M2 × 8 mm screws and two M2 nuts. The frame is stuck to the microscope stage with double-sided tape. The tilt angle is held by how tightly the axis screws are done up: aim for the point where **the plate moves when you push it and stays at that angle when you let go**.

With this stage, skip option B below and go to *2-2. Capture Sequence*. Wherever the steps below say to level the section with a weight, move the main plate by hand instead.

#### B. If you do not have a 3D printer

Build a simple tilting jig from a board and double-sided tape. One example is shown below.

{{< img src="images/page/acquisition/pic6.svg" width="70%" >}}

**Materials**
- Thin section measuring 50 mm × 30 mm (thickness ≤ 0.03 mm)
- Weights totalling a few dozen grams
- A smooth board about 3.5–4.5 mm thick (overall size can be a few centimetres)
- Double-sided tape cut into strips about 1 mm wide

**Assembly**

1. Stick a strip of double-sided tape to the edge of the board and remove the backing.

   {{< img src="images/page/acquisition/pic4.svg" width="70%" >}}


   {{< notice example >}}
   The author stacks three new thin sections, tapes them together, and applies the narrow tape on top. That combination stabilises the pivot height and grip so the section stays in place.

   {{< img src="images/page/acquisition/pic5.jpg" width="70%" >}}
   {{< /notice >}}

3. Place the thin section so that the area of interest sits close to the hinge (the tape) without touching the board.

   {{< img src="images/page/acquisition/pic7.svg" width="70%" >}}

{{< notice example >}}
The photo shows the tilted thin section on the microscope stage. A weight keeps the angle fixed; here a hex wrench is used.

   {{< img src="images/page/acquisition/pic10.jpg" width="70%" >}}

   Figure: Tilted setup

   {{< img src="images/page/acquisition/pic11.jpg" width="70%" >}}

   Figure: Horizontal setup with the weight applied
{{< /notice >}}

### 2-2. Capture Sequence

Record the following five videos in order. Rename each file immediately after recording.

For the tilted recordings, lower the E side of the thin section when the stage is at 0°, and lower the NE side when the stage is at 45°. Before recording Videos 1 and 2, confirm that the tilt stage is oriented as shown below.

{{< img src="images/page/acquisition/coordinate-stage.png" width="90%" alt="Tilt-stage orientations at stage positions of 0 and 45 degrees" >}}

Figure: Tilt-stage orientation. In (a), the E side is lowered with the stage at 0°. In (b), the NE side is lowered with the stage at 45°.

{{< img src="images/page/acquisition/pic8.svg" width="100%" >}}

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
    <source src="{{< url "images/page/acquisition/pic9-0deg-tilt.mp4" >}}" type="video/mp4">
</video>

#### Video 2: With Compensator, Tilted Section, Stage at 45°

1. Rotate the stage to 45° and focus on the bottom-left edge in the monitor view.

{{< notice warning >}}
Because the image is inverted, this corresponds to the top-right edge on the stage.
{{< /notice >}}

2. Start recording and move focus away from the objective for roughly 10 seconds. Stop when the monitor shows the top-right edge in focus (diagram b).

<video controls width="70%">
    <source src="{{< url "images/page/acquisition/pic9-45deg-tilt.mp4" >}}" type="video/mp4">
</video>

#### Video 3: With Compensator, Horizontal Section, Stage at 45°

1. Add the weight to level the section and focus on the area of interest (diagram c).
2. Start recording and stop immediately. A one-second clip is sufficient.

{{< notice note >}}
This clip is used as reference data for the `extinction color` map. As long as you can pair it with the tilted videos, the exact length is unimportant.
{{< /notice >}}

<video controls width="70%">
    <source src="{{< url "images/page/acquisition/pic9-45deg-not-tilt.mp4" >}}" type="video/mp4">
</video>

#### Video 4: With Compensator, Horizontal Section, Stage Rotation

1. Return the stage to 0°.
2. Start recording and, with the weight in place, rotate the stage counterclockwise through 360° (diagram d). About one minute per cycle works well.
3. Stop recording.

<video controls width="70%">
    <source src="{{< url "images/page/acquisition/pic9-xpl-lambda.mp4" >}}" type="video/mp4">
</video>

#### Video 5: Without Compensator, Horizontal Section, Stage Rotation

1. Remove the λ plate.
2. Start recording and rotate the stage counterclockwise through 360° (diagram e) using the same speed as Video 4.
3. Stop recording.

<video controls width="70%">
    <source src="{{< url "images/page/acquisition/pic9-xpl.mp4" >}}" type="video/mp4">
</video>

Save each file with a clear name as soon as the capture ends.
