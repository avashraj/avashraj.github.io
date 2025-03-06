+++
date = '2025-03-03T14:24:15-08:00'
draft = false
title = 'Homography'
+++
**from [CSE185]({{< relref "notes/CSE185.md" >}})**

A homography is a transformation matrix that takes you from one plane to another plane through a point of projection. The
problem we are trying to solve is given a set of matching features/points in 2d images, how can we find a homography that best
agrees with these points?

First when would this homography $H$ be valid?
 - when we are taking images of a plane
 - when the scene is very far(assumed at infinity) so it is a plane
 - when images are taken from the same point


How can we compute $H$?
The homography is a 3x3 matrix that transforms a point from the source image to the destination image. We can only compute 
homography up to a scale factor so even though there are 9 values, we have 8 degrees of freedom. We would stack matching
points on top of each other to form a overdetermined system of equations. The stacked points would be $A$ in the equation, 
$Ah = 0$. We have a constraint $||h||^2 = 1$ so we do not get the trivial solution. We want to minimize $||Ah||^2 \text{ such that }
||h||^2 =1$. With some math:

$$
||Ah||^2 = (Ah)^T(AH) = h^T A^T Ah \text{ such that } h^th = 1
$$

We now make a loss function:
$$
L(h, \lambda) = h^T A^t Ah - \lambda(h^T h - 1)
$$

and derive it to get 

$$
2A^t Ah - 2\lambda h = 0
$$

which is the eigenvalue problem

If we find the eigenvector with the smallest eigenvalue, we have our homography vector h. We can rearrange it to a 3x3 matrix
to get $H$. 

Overall we
1) use SIFT to get features
2) find matching features between the two points
3) make A by stacking source and destination image points
4) find the eigenvector with the smallest eigenvalue to get $H$



