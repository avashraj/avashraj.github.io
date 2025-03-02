+++
date = '2025-03-01T19:45:43-08:00'
draft = false
title = 'Hough Transform'
+++
**from [CSE185]({{< relref "notes/CSE185.md" >}})**

**from [Mar 01 2025]({{< relref "journal/mar-01-2025.md" >}})**

The **hough transform** is one way to find lines in images. It can be done after edge detection because we need an edge map.
It can withstand edges not being connected and objects not being completely in the image. The problem is given edge points
for an image, how can we find lines?

First we can think of the line equation
$$
y = mx + b \Leftrightarrow b = y - mx
$$

The original equation is in terms of x and y while the new one is in terms of m and b. This is because for every point in 
the edge map we know its x and y values. This new equation/space is the **hough space**. Interesting things happen with 
points and lines going back and forth from the image space(OG x,y space) and the hough space. 
 - a point in the image space is a line in the hough space
 - a line in the image space is a point in the hough space

If we have many points that should lie on the same line, those points in image space(lines in hough space) should meet at a
point. This point is the line we are searching for. We want to find the point in hough space with the greatest number of 
intersections. There is a problem though. The slope m can be any real number from $-\infty \leq m \leq \infty$ This will 
create a massive accumulator array(i havent gotten to it yet but i will). We need a different equation to represent lines. 
We can use polar coordinates with 
$$d = xcos(\theta) + ysin(\theta)$$
Now points in image space make sin curves in hough space. Points in hough space are still lines in image space. 
To do this algorithmically we
 - initialize the accumulator array which is where we track the sin curves in hough space
 - for each edge point, add one to its sin curve in the accumulator array
 - the point $Hough(d, \theta)$ corresponds to the line $d = xcos(\theta) + ysin(\theta)$ that we are looking for

This also applies to circles. If we know the radius we can parameterize circles as:
$$
Image(x,y) = (x - a)^2 + (y - b)^2 = r^2 \Leftrightarrow (a - x)^2 + (b - y)^2 = r^2 = Hough(a,b)
$$
The same strategy applies to get the circle, we take the point with the greatest number of intersections. If we do not know 
the radius, we have to add r as a parameter too. This would make a cone in hough space. The more parameters, the bigger our
accumulator arrays become and our strategy becomes less efficient
