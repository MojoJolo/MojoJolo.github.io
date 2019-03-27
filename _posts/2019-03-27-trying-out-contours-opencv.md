---
layout: post
title: "Trying Out Contours on a Climbing Wall using OpenCV"
date: 2019-03-27
---

I'm really interested in learning OpenCV and computer vision before but I don't have an interesting project to work on while learning. Last year, I got into wall climbing as a hobby and I've been spending a lot of time in a climbing gym. Detecting the holds in a climbing wall can be a good OpenCV exercise.

Here's an example of a climbing wall:

<img src="/assets/contours/3_0.jpg" class="rounded mx-auto d-block" alt="Climbing wall example" width="500px">

I heard from colleagues that **contours in OpenCV** might do the task that I wanted. Contours in OpenCV joins the points with the same colors or intensity. With it, I think it can separate the holds into wall.

I tried this experiment in a Jupyter notebook. I uploaded the notebook in a Github Gist and can be seen in this [link](https://gist.github.com/MojoJolo/204a227ef8153caea20eb12a0340a5ea).

There are four essential parts in this experiment. First is converting the image into **grayscale** as contour detection only works for grayscale images.

<img src="/assets/contours/3_1.jpg" class="rounded mx-auto d-block" alt="Grayscale image" width="500px">

Second, I applied **Gaussian Blur** to smoothen the images. This prevent small or unnecessary portion of the image to be detected as contour.

<img src="/assets/contours/3_2.jpg" class="rounded mx-auto d-block" alt="Blurred image" width="500px">

Third, I applied thresholding to seperate portion of the images. In this case, I used **binary plus otsu thresholding**. In the notebook, I tried combining thresholding methods but the result of adding binary and otsu looks better than the others.

<img src="/assets/contours/3_6.jpg" class="rounded mx-auto d-block" alt="Threshold image" width="500px">

Fourth, I filtered the contours. I don't want to small and noise contours to be included that is why I filtered them with an arbitrary number. Contours with very large area will also be filtered because they are most likely to be not a climbing hold. Here's the end result of this experiment:

<img src="/assets/contours/3_9.jpg" class="rounded mx-auto d-block" alt="Final image" width="500px">

A lot of improvement is still needed but I think the end result is good enough for a few lines of code. My next step might be to check if neural nets can drastically improve the accuracy of the detection. I'm planning to learn neural nets and Caffe soon to test this experiment.