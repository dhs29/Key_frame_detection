Platform.ai is an incredible tool that makes it easy for anyone to quickly label large datasets of images. But wouldn't it be great if platform.ai could also work with a similarly popular type of media – video? Support for video would be especially useful since it is more complicated to work with video compared to just images.

Working with videos instead of images presents unique challenges. Larger file sizes require more processing power and storage. Successive frames are likely to be similar, leading to high correlations between images within a video - which can magnify bias in a model. Representing the salient content of several videos on a screen all at once presents UI challenges.

A simplified way to handle videos is to treat them as an unordered collection of image frames to be loaded into platform.ai. Of course, we can't load every single frame since a 2-minute video typically contains up to 3600 images (30 frames per second * 120 seconds = 3600 frames). By assuming that very little happens in the span of a few seconds, we can drastically reduce the number of images. For our baseline model, we chose to keep 1 frame every 2 seconds, which represents a 2-minute video down in 60 images. This frame rate was chosen because YouTube displays one frame every two seconds for the preview when you hover the cursor over the scrollbar - in the author's subjective experience, this is usually good enough to locate a particular section of video.



Pixel Distance
The absolute values of the pixel difference of successive frames gets summed up giving us an indication of change over time. If the change is too little and the value drops below a certain threshold we merge frames to a segment. The middle frame is used to represent the whole segment.


Histogram Distance
The Histogram Distance method is similar to the Pixel Distance method, but instead of calculating the difference using the pixel values, the histogram of the gray-scale of each frame is computed first and the difference of histograms is used.

Here the threshold value was chosen to be the sum of the mean and standard deviation but this can be adjusted to get the preferred number of key frames.
