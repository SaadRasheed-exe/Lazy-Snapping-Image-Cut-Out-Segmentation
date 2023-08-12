# Lazy Snapping Image Cut-Out / Segmentation

This repository contains an implementation of the Lazy Snapping algorithm, a basic interactive image cut-out and segmentation approach. The algorithm utilizes partial human annotations provided as foreground and background "seed" pixels marked with red and blue brush-strokes, respectively. The goal is to compute a precise figure-ground segmentation based on these annotations.

## Implementation Steps

1. **K-Means Clustering**: The first step is to write a function that performs K-Means clustering on color pixels. The function takes the desired number of clusters `k` and the data points to cluster as input. It outputs a cluster index for each input data point and the K cluster centroids.

2. **Seed Pixel Extraction**: Next, the algorithm extracts the seed pixels for each class (foreground and background) and uses the K-Means function to obtain N clusters for each class. A recommended value for N is 64, but experimentation with smaller or larger values is encouraged.

3. **Cluster Likelihood Calculation**: For a given pixel `p` and a specific class (foreground or background), the algorithm computes the likelihood of `p` belonging to each of the N clusters using an exponential function of the negative Euclidean distance between the cluster center `Ck` and the pixel `Ip` in the RGB color space. The overall likelihood `p(p)` of the pixel belonging to this class is a weighted sum of all the cluster likelihoods.

4. **Pixel Assignment**: Finally, each pixel is assigned to the class to which it is more likely to belong. If `p_fg(p) > p_bg(p)`, the pixel `p` is assigned to the foreground class (`x_p = 1`), and vice versa.

## Results and Comparison

The repository includes the implementation of the Lazy Snapping algorithm and provides results for all test images. The results include comparisons of different cases, such as test images with two stroke images, and variations in the number of clusters (`N`) for foreground and background classes.

It is recommended to experiment with different values of `N` and evaluate the impact on the segmentation results. Additionally, the results obtained by the implementation of the K-Means algorithm will be compared against built-in or library functions to assess their effectiveness.

For more details and in-depth analysis, please refer to the reference paper:

- Y. Li, J. Sun, C.-K. Tang, and H.-Y. Shum. "Lazy snapping." In ACM SIGGRAPH 2004 Papers, pages 303–308, 2004.

Explore this repository to gain insights into the Lazy Snapping algorithm and its application in interactive image cut-out and segmentation tasks.
