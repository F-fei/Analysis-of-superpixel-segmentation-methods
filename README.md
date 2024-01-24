# Analysis-of-superpixel-segmentation-methods
## Superpixel extraction methods(SLIC)
## Introduction
In the field of computer vision, superpixels have been widely used as an effective means of image segmentation in various image processing and analysis tasks. Superpixels simplify the complexity of an image by clustering neighbouring pixels with similar features to form larger, meaningful regions while retaining key structural information. Superpixel segmentation methods are mainly classified into two categories: graph-based and clustering-based. SLIC is a popular method for superpixel extraction, which efficiently generates superpixels tightly connected to the image boundaries by a modified k-means clustering algorithm. SLIC's main advantages are its efficient computational performance, low memory requirements, and simple and intuitive operation. In addition, the SLIC method demonstrates excellent boundary adherence and segmentation performance in a variety of benchmark tests, making it a leader among current superpixel algorithms.
## Methodology
In this study, the extraction of superpixels is achieved using the SLIC method, which is a superpixel generation technique based on the improved k-means clustering algorithm.

 Firstly, k clustering centres are uniformly distributed on the image during the initialisation phase. To ensure that the superpixels are roughly equal in size, these centres are sampled along a grid at regular intervals. Then, the pixels are assigned to the nearest cluster centre by calculating the weighted distance of each pixel from the cluster centre. This distance not only takes into account colour differences, but also incorporates spatial proximity, resulting in a balance between colour similarity and spatial proximity. A key innovation of the method is to limit the search to a region proportional to the size of the superpixel, thus significantly reducing the necessary distance calculations and improving the efficiency of the algorithm. During the iteration process, the clustering centres are continuously updated according to the mean value of the pixels belonging to them until convergence. Finally, a post-processing step ensures the connectivity of the superpixels and refines the segmentation results.
## Data
In this experiment we used the Berkeley Segmentation Dataset 500 (BSDS500). The dataset consists of 500 natural images, ground-truth human annotations and benchmarking code. The data is explicitly separated into disjoint train, validation and test subsets. 
## Result

Through our eyes, we can see that pixels of similar colours and similar features are almost nicely assigned to the same superpixel. But is this really perfect? For this reason, we did a quantitative evaluation.
## Evaluation
### Évaluations quantitatives
In the performance evaluation of superpixel extraction, the SLIC method performs well in Boundary Recall, effectively detecting most of the true edges on the image boundary. This metric reflects the SLIC method's ability to maintain the integrity of the image boundary, which is particularly important for applications that require accurate boundary segmentation. 

![BR = \frac{\text{Number of pixels in the corresponding contour}}{\text{Total number of pixels in the true contour}}](https://latex.codecogs.com/svg.latex?BR%20=%20\frac{\text{Number%20of%20pixels%20in%20the%20corresponding%20contour}}{\text{Total%20number%20of%20pixels%20in%20the%20true%20contour}})

Next, in terms of Undersegmentation Error, SLIC also exhibits a low error rate, indicating that its generated superpixels are effective in maintaining object integrity, reducing the leakage of superpixels beyond the object boundary. 

![UE = \frac{1}{N} \sum_{i=1}^{N} \frac{\text{Number of missing pixels in region i}}{\text{Surface of zone i}}](https://latex.codecogs.com/svg.latex?UE%20=%20\frac{1}{N}%20\sum_{i=1}^{N}%20\frac{\text{Number%20of%20missing%20pixels%20in%20region%20i}}{\text{Surface%20of%20zone%20i}})

Finally, SLIC performed mediocrely in our code in terms of Runtime, which may be due to the fact that I work on Googlecolab.

![evaluation_BR_UE.png](https://github.com/F-fei/Analysis-of-superpixel-segmentation-methods/blob/537052a838894b3ae8260af2353846d0892003a9/evaluation_BR_UE.png)

At a superpixel number of 2000, we achieve a BR of 0.65 and a UE of 0.026.
[]
When we segmented each image, the average running time was 16.4 seconds.

###  Comparison with Robin's SLIC
We then compared our results with RobinSLIC, a method from a paper called Bilateral K-Means for Superpixel Computation. There are three main changes in RobinSLIC: gradient correction at initialisation, bilateral distances, connectivity enforcement, and runtime optimisation.

【】
We can look at these two results and overall, there is not much difference, but in some details, RobinSLIC is better. And it is even more surprising in the quantitative assessment.
【】
In the table of BR we can see that when the number of superpixels is 2000, the difference in BR between our method and Ronbin's method is 0.21, and the difference increases as the number of superpixels increases; In the table of UE we can see that when the number of hyperpixels is 2000, the difference between the UE of our method and Ronbin's method is 0.054 and the difference decreases as the number of hyperpixels increases.But in terms of runtime, Robin's segmentation is particularly fast. We picked ten images to compare, and Robin was on average 16 seconds faster than our SLIC. I think this may be due to the fact that I'm running the code on Googlecolab.

## Conclusion
We have carried out superpixel segmentation with interesting results, for example, acceptable values for BR, UE and runtime. However, Overall, SLIC_Robin performs better than Notre_SLIC, especially in the Runtime.

To work on the future, we need to improve the efficiency of our algorithm, especially in the Runtime. Then we need to focus on the details that can be improved, the clustering method, the distribution of pixels, and so on. We also need to focus on using SLIC in conjunction with other tools, such as deep learning.

## Reference

[1] Achanta, R., Shaji, A., Smith, K., Lucchi, A., Fua, P., & Süsstrunk, S. (2012). SLIC superpixels compared to state-of-the-art superpixel methods. IEEE Transactions on Pattern Analysis and Machine Intelligence, 34(11), 2274-2282.https://doi.org/10.1109/TPAMI.2012.120

[2] Gay, R., Lecoutre, J., Menouret, N., Morillon, A., & Monasse, P. (2022). Bilateral K-Means for Superpixel Computation (the SLIC Method). Image Processing On Line, 12, 72-91. [https://doi.org/10.5201/ipol.2022.373](https://doi.org/10.5201/ipol.2022.373)

[3] Jampani, V., Sun, D., Liu, M.-Y., Yang, M.-H., & Kautz, J. (2018). Superpixel Sampling Networks. In Computer Vision – ECCV 2018: 15th European Conference, Munich, Germany, September 8–14, 2018, Proceedings, Part VII (pp. 363–380). doi:10.1007/978-3-030-01234-2_22

[4] D. Martin and C. Fowlkes and D. Tal and J. Malik, A Database of Human Segmented Natural Images and its Application to Evaluating Segmentation Algorithms and Measuring Ecological Statistics, Proc. 8th Int'l Conf. Computer Vision, 2001, July, 2, 416--423
