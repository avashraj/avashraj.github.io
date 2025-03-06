+++
date = '2025-03-02T14:13:45-08:00'
draft = false
title = 'Epipolar Geometry'
+++
from [Computer Vision]({{< relref "notes/CSE185.md" >}})

Similar to triangulation, we can find the point in a 3d world with two images capturing that 3d scene. How tho? The problem 
is: given two images of our scene, the camera matrices $M$ and $M'$ how can we find the irl point $P$?
If we draw rays from the image point in img1 and rays from image point in img2, they will not exactly meet at $P$. We can
take a linear approach and solve for the points closest to both of the rays and P. 

Epipolar geometry is how two images capturing the same point relate. We have the camera centers $C$, $C'$, their image planes,
the point $P$ in space, and the associate image points $x$ and $x'$. All of these lie on a common plane $\pi$

**baseline** - the line joining the two camera centers

**epipole** - the point of intersection of the baseline with the image plane

**epipolar plane** - an epipolar plane contains a baseline

**epipolar line** - the intersection of an epipolar plane with the image plane

If the two cameras face the same direction, and the images are just translated to the left and the right, the intersection
of the baseline with the image plane is at infinity. All epipolar lines are parallel and the epipoles are at infinity. 
Stereo correspondence is finding matching pairs of points in two images taken from slightly different viewpoints. It asks
the question, which point in the left image corresponds to the point in the right image?

Epipolar geometry gives us an advantage because a point on img1 of $P$ can only be on the epipolar line $l'$ 

