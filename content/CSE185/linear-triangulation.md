+++
date = '2025-03-02T13:29:31-08:00'
draft = false
title = 'Linear Triangulation'
+++
**from [CSE185]({{< relref "notes/CSE185.md" >}})**

Imagine a scene like a library. We have a camera taking a picture of the scene. We displace the camera to the right by 
**d** and take another picture of the scence. How can we estimate the coordinates of a point on the scene in terms of the 
axis where both of the cameras lie, and the depth of the image or how far in front of the camera the point is?

First some notation: $(X,Z)$ the irl point we are trying to find, $d$ the baseline or the displacement of the second camera
from the first, $x_L$ and $x_R$ the center of their associated image at a distance $f$ in front of the cameras. If we rewrite
$x_L$ and $x_R$ in terms of the other variables we would get
$$
x_L = f \frac{X}{Z} \\
$$
$$
x_R = f \frac{X - d}{Z}
$$

If we keep doing some freaky algebra we would get
$$
X = x_L \frac{d}{d'}
$$
$$
Z = f \frac{d}{d'}
$$

here d' is the disparity. Disparity is the difference in pixel locations of the scene we are capturing in the two images. We
can visualize this by holding a finger in front of our eyes and closing one eye. If we close our open eye and open the other
we can see a shift in position of our finger. 

We know that the point in our images is equal to our camera matrix multiplied to the real world point. Some more notation is
$\tilde{x}$ and $\tilde{x'}$ are our image points, $P$ and $P'$ are our camera matrices, and $\tilde{X}$ is our real world 
point. 

$$\tilde{x} = P \tilde{X}$$
$$\tilde{x'} = P' \tilde{X}$$

If we take the cross product of $\tilde{x}$ and $P \tilde{X}$ we woulto make it a 4x1 matrixd get 0 because these values are collinear(idk what that 
means yet). Theres this cool trick where if we expand the cross product, we are able to reduce one row because it is 
in terms of another row. (I am too lazy to write the latex to show that right now i got way more to study). 
We can now rewrite this in the form of $Ax = 0$. If we do this to the other image, we can combine the As from both images.
This is the overconstrained problem for the null space where we can take the SVD to get the eigenvector with the smallest
eigenvalue. This vector is our $\tilde{X}$. This was all in 2D though. 
