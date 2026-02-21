# BMW Cinematic Trailer (Unreal Engine)

A cinematic showcase project built in **Unreal Engine 5**, focused on presenting a BMW vehicle through dynamic shots, procedural vehicle motion, and multi-camera direction using the **Level Sequencer** pipeline.

## 🎬 Final Trailer

Watch the final cinematic here:  
[YouTube – BMW Cinematic Trailer](https://youtu.be/bj3E0eKvoVI)


## Project Goal

To create a professional and visually engaging cinematic trailer that highlights Unreal Engine’s real-time rendering, vehicle rigging, and cinematic direction capabilities through coordinated scene transitions and camera work.


## Core Features

* Skeletal vehicle built from multiple static components
* Procedural animation using Control Rig
* Suspension simulation with spring interpolation
* Steering and wheel rotation system
* Multi-camera cinematic direction
* Spline-based camera motion (CameraRig Rail)
* Animation refinement using Curve Editor
  

## Implementation Overview

### 1. Vehicle Construction (Skeletal Mesh)

The vehicle is constructed as a **Skeletal Mesh** to allow independent movement of components such as wheels and suspension.

**Workflow:**

1. Align and assemble vehicle parts in the viewport.
2. Create a skeleton with a proper bone hierarchy.
3. Bind each movable component to its corresponding bone.
4. Apply Skin Weight Painting to isolate deformation influence.

The result is a single optimized skeletal asset suitable for procedural control and cinematic animation.


### 2. Procedural Control System (Control Rig)

A **Control Rig** is used to procedurally drive vehicle behavior.

#### Suspension System

* A Line Trace is performed from each wheel toward the ground.
* The detected distance determines vertical suspension offset.
* A Spring Interpolate node adds elastic behavior.
* Alpha interpolation smooths transitions.

#### Steering System

* Front wheel bones rotate based on a steering control.
* A coefficient limits maximum steering angle.

#### Wheel Rotation

* Linear travel distance is converted into angular rotation.
* Rotation values are injected into wheel bones per frame.

Viewport control handles (X/Y/Z axes) are used for animation authoring and are not visible in final renders.


### 3. Level Sequencer Integration

**Level Sequencer** is used to orchestrate animation and direction.

* The vehicle is added to a sequence.
* A Control Rig track is attached.
* Keyframes are created for steering, body motion, and wheel rotation.
* Sequencer streams values to the Control Rig in real time.

This allows procedural systems to remain dynamic while being directed cinematically.


### 4. Cinematic Cameras

The trailer uses multiple **Cine Camera Actors** controlled via a **Camera Cuts** track.

#### CameraRig Rail

* A spline defines a smooth camera path.
* The camera attaches to the rail.
* The "Current Position on Rail" parameter (0–1) is animated in Sequencer.

This ensures stable, cinematic tracking and orbit shots.


### 5. Curve Editor Refinement

The Curve Editor is used to:

* Convert linear interpolation into eased motion.
* Synchronize multiple axes.
* Adjust acceleration and deceleration via tangent handles.

Parameter visualization typically maps axes to color-coded curves (X, Y, Z) for clarity during refinement.

### 6. Rendering

The cinematic was rendered using Unreal Engine’s **Movie Render Queue**:

* Exported the sequence as high-quality image frames
* Imported the image sequence into DaVinci Resolve
* Edited and color graded the footage
* Exported the final video as `.mp4`

