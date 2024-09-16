# CS195-Fall24-Notebook-2
## Simple Neural Network: MLP and CNN!

<b>Due</b>: Monday, September 23th, 2024

## How this is going to work: 

I've provided some starter code for you. Before you go any further, click on the `notebook2_mlp_starter.ipynb` and `notebook2_cnn_starter.ipynb` links in the repository, and then, at the top of the notebook, you will see a button that says `Open in Colab`. Click on this and it will open the starter code in Google Colaboratory.

## The Images
For this notebook, you will need the following two images:
- **Image#1**: [this link](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/data/first_photograph.png). *Use this for Task#1*
- **Image#2**: [this link](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/data/himalaya_dark.jpg). *Use this for Task#2*
 
First things first: upload the images to your Google Drive and then mount your Drive to the notebook. I aim to help everyone get familiar with the programming environment and comfortable working with pixel values in images. There will be two tasks: you'll perform various per-pixel transformations on images and observe the results.
# **Task#1**: Whitening Transformation
You will be adjusting the contrast of the image. Your goal is to transform the image so that the resulting image has a zero mean and unit variance. Denote the image as $I(.)$ which is a 2D array of pixel values. Its width and height are $N$ and $M$ pixels respectively. Also $I(x,y)$ denotes the pixel value at 2D location $(x,y)$.

## **Step 1:** 
You can compute the mean and variance of the gray-scale image $I(.)$ as follows:

<!--$\mu$ = $\frac{\sum_{x=1}^{N}\sum_{y=1}^{M}I(x,y)}{N \times M}$
\sigma^{2} = \frac{\sum_{x=1}^{N}\sum_{y=1}^{M}(I(x,y)-\mu)^2}{N*M}-->
![mean and variance equations](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/etc/whitening_eq1.png)

## **Step 2:** 
Now, you can transform each pixel value separately using the above two computed statistics $\mu$ (mean) and $\sigma$ (standard deviation) as follows:
    <!--I^{'}(x,y) = \frac{I(x,y)-\mu}{\sigma}-->
    
![whitening transformation](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/etc/whitening_eq2.png)


Apply this *Whitening Transformation* on the provided input image to see how it affects. The following figures show the effect of applying *Whitening Transformation* on the first-ever photograph -- **Image#1**: [this link](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/data/first_photograph.png). The result should something like below:

![Result task#1](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/etc/task1_result.png)

# **Task#2**: Histogram Equalization
Let’s try a different contrast transformation called Histogram Equalization on the input image. This process involves multiple steps. You only need to complete the first three steps. I've provided a code snippet for step #4. If you correctly implement steps 1, 2, and 3, your code should brighten the darker regions of the image. 
Once you finish the steps, apply your code on **Image#2**: [this link](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/data/himalaya_dark.jpg) to observe its impact. 

## **Step 1:** 
You need to create a histogram of the intensity values in an image. The easiest way to do this is by using the Pillow Library (TIP: There’s a function called histogram() in the Pillow Library that can help). There can be up to 255 different intensity values for a grayscale image. Let’s represent the histogram as a 1D vector, where each element is denoted by $hist_{b}$, corresponding to a bin for an intensity value $b$. The value of $b$ ranges from 0 to 255.

For each intensity value $b$, count how many pixels in the image $I(.)$ have that exact intensity, and place that count in the corresponding bin, $hist_{b}$. If we repeat this process for every intensity value, starting with $b = 0$ and going up to $b = 255$, we obtain the final histogram as a 1D vector: $hist$ = [ $hist_{0}$, $hist_{1}$, $hist_{2}$, ..., $hist_{255}$]. Here's the histogram generated for a grayscale image:

![histogram](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/etc/histogram_example.png)

Notice in the image above that all the bin values for intensities of 120 or higher are zero. This means that no pixels in the image have an intensity greater than 120. That's why the image appears so dark—most of the pixel intensities are grouped between 0 and 120.

## **Step 2:**
Now you need to normalize the histogram $hist$ such that the sum of this new histogram is equal to 255. Denote this new histogram as $hist^{'}$. For each bin $b$, you can compute it as follows:

![histogram normalization](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/etc/histogram_equalization_eq1.png)

Recall that the image width and height are $N$ and $M$ pixels respectively. The shape of the normalized histogram should look the same as the original histogram (as shown below). However, if you add up all the bin values in your normalized histogram, the total should be 255, since you've normalized it using the equation above.

![histogram](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/etc/histogram_normalized.png)

## **Step 3:** 
Compute the cumulative sum of the $hist^{'}$. Denote this histogram as $histcum^{}$. Let's say you have histogram with 4 bins with the following values $[1,2,3,4]$. In this case, you have a histogram with 4 bins, and the frequency values of these bins are given such that
*the first bin contains 1*, *the second bin contains 2*, *the third bin contains 3*, and *the fourth bin contains 4*. The cumulative sum involves progressively adding the values of the histogram bins as you move from the first bin to the last. Essentially, each entry in the cumulative sum array represents the sum of all previous bins' values plus the current bin's value. Cumulative sum of this histogram would be $[1,3,6,10]$. If you correctly compute cumulative sum of the $hist^{'}$ they result should look something like this:

![histogram](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/etc/histogram_cumulative_sum.png)

## **Step 4:** 
Use the cumulative histogram $histcum^{}$ as a lookup table to transform the value of each pixel location as follows:

![color lookup](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/etc/histogram_equalization_eq2.png)

where $I^{'}(x,y)$ denotes the histogram equalized image value at pixel location $(x,y)$. 

Apply your *Histogram Equalization* implementation on **Image#2**: [this link](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/data/himalaya_dark.png) to observe its impact on the **Himalaya image**. The following figures show the result:

![Result task#2](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/etc/task2_result.png)

> *I've provided a code snippet for this step (see `notebook1_histogram_equalization_starter.ipynb`). You do not need to write code for this step. If you correctly implement steps 1, 2, and 3, your code should brighten the darker regions of the image.*

Use the two starter notebooks to finish the implementations. Submit this assignment through the CodePost link (find it on Blackboard).

## :white_check_mark: Grading: 
I will update the following rubric with your grade after you have completed the assignment.

### Rubric:
> *This assignment is worth 5 points. I will gladly add an extra 0.5 points if you can find another low-intensity image and enhance its brightness using your histogram equalization method!*

>

| Exercise #  | Points Awarded (out of 5)  | Notes |
| --------- | ------------------- | --------- |
| 1:  whitening transformation         |    -/2.5    |            |
| 2: histogram equalization            |    -/2.5    |            | 
| <b>Total                             |    -/5      |     </b>   |
