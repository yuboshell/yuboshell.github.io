---
layout: homepage
---

<style>
.mc-demo { margin: 1.5rem 0 2rem; }
.mc-demo video { width: 100%; height: auto; display: block; background: #000; }
.mc-demo figcaption { font-size: 0.85rem; color: #6b6b6b; margin-top: 0.55rem; line-height: 1.5; }
.mc-demo figcaption b { color: #333; }
.mc-specs { font-size: 0.95rem; color: #333; margin: 0.4rem 0 1.4rem; }
</style>

<p style="margin-bottom:1rem;"><a href="/">&larr; Home</a></p>

## Motion Capture and 3D Reconstruction <span style="color:#e74d3c; font-weight:600; font-size:0.66em; white-space:nowrap;">[ Looking for collaborators! ]</span>

I work on the motion-capture side of 3D vision: building a system that records the 3D motion of articulated subjects, people, animals, and sometimes objects, to produce the ground-truth data that downstream 3D models are trained and evaluated against. This data is scarce and expensive to obtain, and high-fidelity 3D annotation matters more here than algorithmic novelty. To keep the annotations trustworthy enough to serve as ground truth, the pipeline avoids learning-based shortcuts. The long-term aim is model-free reconstruction of arbitrary subjects.

**How can high-fidelity motion capture leave the studio?** Our answer is a fully mobile, markerless rig of eleven commodity smartphones, deployable in the wild: outdoors, in barns, and in unprepared indoor spaces. It runs in three stages: per-frame inter-camera synchronization, multi-view camera calibration, then application-specific reconstruction.

<p class="mc-specs"><b>Eleven Google Pixel 7 phones · 4K · 30 fps · under 17 ms inter-camera sync</b></p>

### Demo 1: Dairy-cow reconstruction (model-free)

<figure class="mc-demo">
  <video src="./assets/videos/cow-reconstruction.mp4" autoplay loop muted playsinline controls preload="metadata"></video>
  <figcaption><b>Arbitrary-object reconstruction</b> on a moving Holstein cow in the barn. Left: a raw camera view from the rig. Right: the reconstructed 3D point cloud with the recovered camera poses, orbiting around the cow. Pipeline for the object track: SAM 3 foreground masks, COLMAP structure-from-motion, then ACMMP dense multi-view stereo. No body model, no learned priors.</figcaption>
</figure>

### Demo 2: Human pose estimation

<figure class="mc-demo">
  <video src="./assets/videos/human-pose-smplx.mp4" autoplay loop muted playsinline controls preload="metadata"></video>
  <figcaption><b>SMPL-X fitting</b> for the human-pose track. Multi-view 2D keypoints (MMPose) are triangulated across the eleven views, then refined by SMPL-X fitting with silhouette supervision. SMPL-X is a parametric fallback, used here only because no model-free alternative exists yet for human bodies.</figcaption>
</figure>

### The system in brief

- **Synchronization:** software-only, no hardware trigger; under 17 ms offset across the eleven-phone rig. Capture runs through Argus, our Android app for the rig.
- **Calibration:** a moving chessboard, Zhang intrinsics, PnP extrinsics, then COLMAP bundle adjustment. About 1 px reprojection error, roughly 2 mm in metric terms.
- **Reconstruction:** human pose (MMPose, triangulation, SMPL-X fitting) or arbitrary objects (SAM 3 masks, COLMAP SfM, ACMMP dense MVS).

A two-page visual summary, with the full pipeline and references, is here: [Motion Capture and 3D Reconstruction work summary (PDF)](https://github.com/yubohuangai/Motion-Capture/blob/master/share/Motion_Capture_and_3D_Reconstruction_Work_Summary.pdf). Code lives in [Motion-Capture](https://github.com/yubohuangai/Motion-Capture) (calibration, reconstruction, pose) and [Argus](https://github.com/yubohuangai/Argus) (synchronization).

### Work with me

As a technology nerd, I love trading ideas with curious people and sharing the engineering skills and thinking I have picked up along the way. I am happy to mentor you hands-on until you are up to speed. If this project interests you, or you would simply like to collaborate, please do not hesitate to get in touch.

Reach me at <a href="mailto:yubo16@ualberta.ca">yubo16@ualberta.ca</a>.
