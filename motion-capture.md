---
layout: default
title: Motion Capture & 3D Reconstruction
---

<style>
.mc-body { padding: 0 2.5%; }
.mc-body h2 { margin-top: 1.2rem; }
.mc-body h3 { display: block; margin: 1.4rem 0 0.4rem; }
.mc-demo { margin: 1.5rem 0 2rem; }
.mc-demo video { width: 100%; height: auto; display: block; }
.mc-demo figcaption { font-size: 0.85rem; margin-top: 0.55rem; line-height: 1.5; }
</style>

<div class="mc-body" markdown="1">

## Motion Capture and 3D Reconstruction <span style="font-weight:600; font-size:0.66em; white-space:nowrap;">[ Looking for collaborators! ]</span>

### Work with me

As a technology nerd, I love trading ideas with curious people and sharing the engineering skills and thinking I have picked up along the way. I am happy to mentor you hands-on until you are up to speed. If this project interests you, or you would simply like to collaborate, please do not hesitate to get in touch.

Reach me at <a class="email-link" href="mailto:yubo16@ualberta.ca">yubo16@ualberta.ca</a>.

### Background

Motion capture records the 3D motion of articulated subjects, people, animals, and sometimes objects, producing the ground-truth data that downstream 3D models are trained and evaluated against. The field is data-bound: high-fidelity 3D annotation matters more than algorithmic novelty, yet such data is scarce and expensive to obtain. To keep annotations trustworthy enough to serve as ground truth, the pipeline avoids learning-based shortcuts. The long-term aim is model-free reconstruction of arbitrary subjects.

### System

How can high-fidelity motion capture leave the studio? The answer here is a fully mobile, markerless rig of eleven Google Pixel 7 smartphones, recording at 4K and 30 fps and synchronized to under 17 ms between cameras, deployable in the wild: outdoors, in barns, and in unprepared indoor spaces. From raw video to reconstruction, it runs in three stages:

- Synchronization: software-only, with no hardware trigger; under 17 ms offset across the eleven-phone rig. Capture runs through Argus, the in-house Android app for the rig.
- Calibration: a moving chessboard, Zhang intrinsics, PnP extrinsics, then COLMAP bundle adjustment, reaching about 1 px reprojection error, roughly 2 mm in metric terms.
- Reconstruction: for human bodies, MMPose 2D keypoints, triangulation, and SMPL fitting; for arbitrary objects, SAM 3 masks, COLMAP structure-from-motion, and ACMMP dense multi-view stereo.

### Demo 1: Cattle reconstruction (model-free)

<figure class="mc-demo">
  <video src="./assets/videos/cow-reconstruction.mp4" autoplay loop muted playsinline controls preload="metadata"></video>
  <figcaption>Arbitrary-object reconstruction on a moving Holstein heifer in the barn. Left, a raw camera view from the rig; right, the reconstructed point cloud with the recovered camera poses, orbiting around it. The object track uses no body model and no learned priors: SAM 3 foreground masks, COLMAP structure-from-motion, then ACMMP dense multi-view stereo.</figcaption>
</figure>

### Demo 2: Human pose estimation (parametric)

<figure class="mc-demo">
  <video src="./assets/videos/human-pose-smpl.mp4" autoplay loop muted playsinline controls preload="metadata"></video>
  <figcaption>Human pose estimation by SMPL fitting. Multi-view 2D keypoints from MMPose are triangulated across the eleven views, then refined by SMPL fitting with silhouette supervision. SMPL is a parametric body model, a fallback used only because no model-free alternative exists yet for human bodies.</figcaption>
</figure>

### Demo 3: IMU motion capture (reproduction of GlobalPose)

<figure class="mc-demo">
  <video src="./assets/videos/imu-mocap.mp4" autoplay loop muted playsinline controls preload="metadata"></video>
  <figcaption>A reproduction of <a href="https://github.com/Xinyu-Yi/GlobalPose">GlobalPose</a> (Yi et al., SIGGRAPH 2025), which recovers full-body motion from six body-worn IMUs with physics-based global motion estimation. Left, the subject wearing the inertial sensors; right, the reconstructed body, shown here at its T-pose calibration. This is a different modality from the camera rig above, a wearable inertial setup rather than multi-view video, included to show breadth; the method and code are the original authors', not mine.</figcaption>
</figure>

### Resources

A two-page visual summary, with the full pipeline and references, is available as a [PDF work summary](/assets/files/Motion_Capture_and_3D_Reconstruction_Work_Summary.pdf). The code lives in [Motion-Capture](https://gitlab.com/huangyubo/Motion-Capture), covering calibration, reconstruction, and pose, with a companion app, Argus, handling synchronization.

</div>
