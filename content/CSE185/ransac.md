+++
date = '2025-03-03T15:46:03-08:00'
draft = false
title = 'Ransac'
+++
**from [CSE185]({{< relref "notes/CSE185.md" >}})**

When we do SIFT, we get a bunch of features on each image. When we get matching features, many of these features may be 
matching according to SIFT, but they do not actually correspond to their respective points on the images. We need a way to
make sure  the models(homography matrices) generated from those matches are actually good.

We can use RANSAC to do this. The steps of ransac are as follows:
1) randomly choose the minimum number of samples needed to fit a model. For homography, we need 4 matching points
2) fit the model/create our homography matrix
3) count the number of datapoints that actually fit the model. the points that fit the model are inliers. 
4) repeat steps 1-3 N times
5) choose the model that has the largest number of inliers
6) recompute the model with all of the inliers

How do we count the number of datapoints that actually fit the model?

**Symmetric transfer error**
$$
d(x,H^-1 , x')^2 + d(x', Hx)^2
$$

This forumla is asking what is the distance between the first point and the inverse homography multiplied by the corresponding
point on the other image. We are trying to find out how "off" our homography was for that point. The second part of the formula
is the same thing. How far off was the actual second point from where we estimated that point to be? We square both of these 
distances and add them to get our symmetric transfer error for a homography that relates two specific points together. 
This method is computationally easier than reprojection but is less accurate

**Reprojection error**
With reprojection, we compute the 3D point that corresponds to a pair of matching image points. We then reproject that point 
back onto both images and calculate the euclidiean distance between the observed and reprojected points. 

