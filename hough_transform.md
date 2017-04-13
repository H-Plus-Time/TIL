# Hough Transform performance
Owing to the 5D parameter space, this is an extraordinarily slow method
for shape detection.

See "A Fast and Robust Ellipse-Detection Method Based on Sorted Merging"
(http://dx.doi.org/10.1155/2014/481312) for details on the current
state-of-the-art algorithms for ellipsis detection.

TLDR: use arc segment merging.
