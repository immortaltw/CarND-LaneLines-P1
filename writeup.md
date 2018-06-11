# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

There are 7 steps in my pipeline:

1. Filter unwanted colors out so that only white and yellow are left in the image.
2. Grayscale the image.
3. Use Gaussian blur to smooth out the image.
4. Use Canny edge detection to get all the edges.
5. Use fillPoly to create a masked image containing only the region of interest.
6. Use Hough transform to find all the "lines" and generate an image with only lines.
7. Finally, overlap the "lined image" with the original image to get the result.

As for the draw_lines() function, I grouped those points that contribute to negative slope into right line group and positive slope to left line group. I also collect both - slopes and + slopes into two lists and take their median as the representatives. For left line I choose the point that has minimum x as a reference point, max x for right line.

With the slopes, representatives points and y limit of both lines, I can plug them into the slope equation and compute the corresponding x points for y limit points of both lines. Then I use the reference points and the points computed as the vertices of the lines and use it to draw lines.

I also tried to apply the pipeline to the challenge problem. It's weird that it worked well with the image I captured from the challenge video but not the case when applying to the video. The result is shown in the notebook. Maybe I need to dive deeper into the video processing library to understand how to correctly deal with videos.

### 2. Identify potential shortcomings with your current pipeline

First of all, I could use different strategy to extrapolate the two lines. Filtering out outlier slopes. Making sure in the video the location and slope of current line can't be too far away from the previous line. These tricks could make the result look better.

Also, in my current pipeline, it involves lots of parameter tuning, which is not likely to be able to adapt to complex real-world environment. It's just simply not going to scale. To me using machine learning to do classification is a better way for this kind of problem. The pipeline is very sensitive to shades. Also, I think the camera angle is another uncertainty.

### 3. Suggest possible improvements to your pipeline

It would be nice if there're more image and video samples that represent different lighting/weather/traffic etc.. Maybe with this information I can create a more generic parameter set to cope with different real-world conditions.
