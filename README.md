# Homographies and Condensation (Particle Filtering)

Python implementation.

Coursework for the module "Machine Vision" of the M.Sc. in Machine Learning (UCL).

## Part1 - Homographies

### Task1: 

We converted 5 points (Cartesian coordinates) into its homogeneus representation and then multiplied by a given Homography matrix to get
the set points number 2 in its homogeneus representation; then we converted those points into its cartesian coordinates. Below on the left,
we see the result where the points in red are the set of points number 2. After that, we applied some noise to the set of points number 2.

<br>
<p align="center">
<img src=misc/homography2.png>
</p>
<br>

We implemented the functions to compute the homography matrix given two points in cartesian coordinates (we need the SVD matrix to get the homography matrix).
We used that function using as arguments the previous set of points number 1 and number 2 (the one with some noise). We used that homography matrix to estimate
the position of the set of points number 2 and converted them to cartesian coordinates. On the figure above (right), we see the plot of the estimate and the real
coordinates of the set of points number 2. The green lines represent the mean squared error.

### Task2: 

we were tasked to apply the homography to make a panorama of images that are related by a homography. First we calculate the 
homography matrix using the points of reference in image 1 (center) and the points from image 2 (left). Then we start a for loop over all 
the pixels in the image 1. We convert the cartesian coordinates of each pixel in their homogeneous representation and then multiplied by 
the homography matrix. After that, we need to convert back to cartesian and then check if the coordinates exist within the dimensions of 
image 1, if so, we copy the color values in the image of thre center. We do the same with the image on the right (the one with the magenta
points). The final result is shown on the bottom.

<br>
<p align="center">
<img src=misc/homography1.png>
</p>
<br>

### Task 3

we are going to take a real image containing a planar black square and figure out the transformation between the square and the camera.
We are given the points needed to estimate the extrinsic matrix, the intrinsic matrix is given too.

In the image below we can see the points projected in green on the left and on the right the wireframe of a cube using those points. 
We can see that the cube is slightly askew, but it has a good shape. This could happen when we extract the first two columns from the 
homography matrix to then apply SVD since this last operation and the closest valid first two columns of a rotation matrix to the first two
columns of the homography matrix. Also, this problem requires nonlinear optimization, however we are getting an approximation by using 
the homogeneous representation.

<br>
<p align="center">
<img src=misc/homography3.png>
</p>
<br>

### Part 2 - Particle Filtering

For this exercise we are going to perform Condensation which is a method to perform Particle Filtering, which is a technique to represent
the probability density as a set of particles in the state space. Particle Filtering deals with the issues in Extended Kalman Filters, 
which cannot deal with multimodal distributions.

First we normalise the weights in order to get a distrbution of the weights. Then, we compute the cummulative distribution of those weights.
After that, we add some noise into the model (Brownian motion model) and normalise the weights again.

<br>
<p align="center">
<img src=misc/condensation.png>
</p>
<br>

We see in the images below that at iteration 0, the particles start at random and then the particles begin to cluster around the green areas.

<br>
<p align="center">
<img src=misc/particle_1.png>
</p>
<br>


<br>
<p align="center">
<img src=misc/particle_2.png>
</p>
<br>

