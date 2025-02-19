+++
date = '2025-02-05T19:55:18-08:00'
draft = true
title = 'First Computer Vision Quiz'
+++

**Computer vision is the science/art of translating images into useful information.**

An image is a matrix or tensor of discrete values ranging from 0 to 255. The number is the intensity of
light captured by a sensor. If you were to look at a picture, a single pixel is represented by one of these numbers. 
Pixels can have one channel (gray scale image where 0 is black and 255 is white) or multiple channels like a rgb image
(0 is black and 255 is the max intensity for that color).

### Homogeneous coordinates and perspective projection
Homogeneous coordinates are another way to represent points and lines. They are equivalent points to their Euclidian counterparts. Typically coordinates are written with n numbers
where n is the dimension. In a plane it is (x,y). Homogeneous coordinates have n + 1 coordinates because it projects that
point onto a higher dimensional space. This would be written as (x,y,w). This has the advantages of being able to translate using matrix multiplication, 
utilize projective geometry, and make perspective projection more natural. 

show homogeneous points in latex

To get an image, we need to be able to project a 3d point to a 2d point. A simple way of doing this is orthographic 
projection. In this system, we assume that all light rays are parallel to the camera's z axis. This way we can just drop
the z axis to go from 3d to 2d. However, we now loose all depth information. If an object is further away, it will not 
appear smaller in the image. 

A better system is **perspective projection**. We now assume that light rays pass through their point in the world, their
corresponding pixel in the image, and the camera's center. We also make sure that the z axis of the camera is aligned with
the z axis of the image. Points in the world are mapped to their point on the image by dividing by the z coordinate and 
multiplying by the focal length(distance from the camera to the image). A **principal point offset** is also added to ensure
all coordinates are positive in the image. 

**How can we map a 3d point in the world to a 2d point in our image?**

We can map a 3d point irl to a 2d point in our picture using a series of matrix transformations. First we need to convert 
from the "world's" coordinate system to the camera's. This can be done with the camera pose or the extrinsic matrix. It 
is a rotation and a translation. Next we need to go from the camera's to the image's coordinates. We do this with the 
(intrinsic) calibration matrix K. After these transformations (which can be computed as one 3x4 matrix) we get to our 
image coordinates.

show intrinsic and extrinsic and k matrix in latex

**What if they camera's coordinate system is different from the coordinate system of the object we are trying to capture?**

**Parallel lines in perspective projection of 3d meet at a vanishing point**
The vanishing point occurs when w = 0 in homogeneous coordinates. These are also called points at infinity. A picture can
have multiple vanishing points, with different lines having different vanishign points. Lines on the same plane have 
points at infinity on the same vanishing line. If we have a line formed by (a1 x a2) and another by (b1 x b2), their
cross product is their vanishing point. 

talk about full camera matrix and show it in latex

An image histogram is a plot of all of the pixels in an image. The x axis is the image intensity and the y axis is the count. 
An image histogram that is shifted to the left is usually underexposed and darker. One that is shifted to the right is usually
overexposed. A gamma compression can be used to show details hidden in dark regions in an image. A gamma value 0-1 makes the
image darker, while a gamma value above 1 makes it brighter.

### smoothing and edge detection
Filtering is an important process in computer vision. It can help with removing noise as well as finding features like edges,
points, or corners. To apply a filter, we use a matrix called a kernel. The kernel is used to perform a convolution. A 
convolution can be imagined as the overlapping of the kernel on top of the image matrix. We take into account the overlapping
cells and compute some value using the original pixel values and the kernel values. 

