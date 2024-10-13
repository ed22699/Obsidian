---
tags:
  - Lesson
  - stereo_and_motion
---
**Stereo**
- determining scene depth information from 2 or more images captured from different viewpoints
- geometry, correspondence matching and 3-D reconstruction
**Motion**
- determining 2-D motion in video frames
- modelling, optical flow and motion estimation

# Stereo Vision
- 3D from two images taken from different viewpoints
- **Parallax** - objets appear in different positions in each viewpoint
	- things closer in a scene move further than those in the distance
- **Disparity** - position of object in each image depends on its depth
	- position difference (disparity) is inversely proportional to depth
	- the further things are away the less far they move in the frame
- if we know disparity and viewpoints we can construct a 3D scene

whats in the scene, where the cameras are can cause problems
- self-occlusion
- shadows and lighting changing appearance (same object looks different)
- different things look the same (hard to lock onto a point)

### Two-view stereo
![[Screenshot 2024-10-13 at 17.42.59.png|300]]
- $d$ is the difference in position between the two cameras
- $d$ is inversely proportional to the depth of that point ($d \propto \frac 1 Z$)
- larger $d$ means a smaller $Z$ (depth)
### Multi-view stereo
![[Screenshot 2024-10-13 at 17.48.34.png|100]]
- generalised two-view stereo
- multi-view stereo, take a video of the scene combine the views to get better estimates
- some views can't see certain points, tricky
## Problems
- **Geometry** - determine relative position and orientation of the cameras
	- geometry of cameras relative to each other ( can use a rig so you do not need to estimate)
- **Correspondence** - determine matching points in the stereo views
	- image processing task
- **Reconstruction** - determine 3D location in scene of matched points via triangulation
>[!note]
all three issues are interrelated, knowing one can help the others

### Geometry
- need to understand geometric relationship between cameras to allow 3D reconstruction from correspondences
![[pin hole camera model]]
#### Simple two-view stereo
- coplanar image planes (COPs in X-Z plane)
- geometry defined by similar triangles
- $T$ - baseline (distance between COPs)
- point $P$ has depth $Z$
- using similar triangles:
	- $\frac T Z=\frac{T-x_L +x_R}{Z-f}$
	- you can manipulate this to: $Z=\frac{fT}{x_L-x_R}=\frac{fT}d$ 
	![[Screenshot 2024-10-13 at 18.11.30.png|200]]
#### General stereo
- geometry depends on position and orientation of cameras
- epipolar geometry
- reminder [[rotation matrices]]


