+++
date = '2025-03-02T15:31:26-08:00'
draft = false
title = 'Fundamental Matrix'
+++
from [Computer Vision]({{< relref "notes/CSE185.md" >}})

The fundamental matrix $F$ is the algebraic representation of epipolar geometry. It is independant of the scene and can be
computed using corresponding points. We don't even need to know the camera intrinsics or extrinsics. There will be a 2d homography
$H_\pi$ mapping each $x_i$ to $x'_i$ where $x_i$ is a point in img1 and $x'_i$ is a point in img2. 

The epipolar line in the image plane $l'$ connects $e'$ and $x'$ can be written as the cross product between the points. We can make a
skew symmetric matrix with $e'$ to make the cross operation part of a matrix multiplication like $[e']_x$. Now

$$
l' = e' \times x' = [e']_x x'
$$

$$
x' = H_\pi x
$$

The benefit is that we can chain the cross products now. The fundamental matrix is the skew symmetric matrix of $e'$ multiplied
to the homography matrix $H_\pi$. If $x$ and $x'$ are corresponding points, $X'^T Fx = 0$. 


$l' = Fx$ is the epipolar line corresponding to $x$. 

$l = F^T e' = 0$ is the epipolar line corresponding to $x'$

$F e = 0$

$F^T e' = 0$

Each corresponding point pair gives one equation and we need at least 7 correspondences to compute F.

$H_\pi$ has rank 3, $[e']_x$ has rank 2, and F has rank 2
