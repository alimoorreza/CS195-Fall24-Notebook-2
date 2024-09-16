# CS195-Fall24-Notebook-2
## Simple Neural Networks: MLP and CNN!

<b>Due</b>: Monday, September 23th, 2024

## How this is going to work: 

I've provided some starter code for you. Before you go any further, click on the `notebook2_mlp_starter.ipynb` and `notebook2_cnn_starter.ipynb` links in the repository, and then, at the top of the notebook, you will see a button that says `Open in Colab`. Click on this and it will open the starter code in Google Colaboratory.
 
# **Task#1**: Multilayer Perceptron (MLP)
You will be adjusting the contrast of the image. Your goal is to transform the image so that the resulting image has a zero mean and unit variance. Denote the image as $I(.)$ which is a 2D array of pixel values. Its width and height are $N$ and $M$ pixels respectively. Also $I(x,y)$ denotes the pixel value at 2D location $(x,y)$.


<!--![mean and variance equations](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/etc/whitening_eq1.png)

![whitening transformation](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/etc/whitening_eq2.png)


![Result task#1](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/etc/task1_result.png)-->

# **Task#2**: Convolution Neural Network (CNN)
Let’s try a different contrast transformation called Histogram Equalization on the input image. This process involves multiple steps. You only need to complete the first three steps. I've provided a code snippet for step #4. If you correctly implement steps 1, 2, and 3, your code should brighten the darker regions of the image. 
Once you finish the steps, apply your code on **Image#2**: [this link](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/data/himalaya_dark.jpg) to observe its impact. 


<!--![histogram](https://github.com/alimoorreza/CS195-Fall24-Notebook-1/blob/main/etc/histogram_example.png)-->


Use the two starter notebooks to finish the implementations. Submit this assignment through the CodePost link (find it on Blackboard).

## :white_check_mark: Grading: 
I will update the following rubric with your grade after you have completed the assignment.

### Rubric:
> *This assignment is worth 5 points.*

>

| Exercise #  | Points Awarded (out of 5)  | Notes |
| --------- | ------------------- | --------- |
| 1: MLP            |    -/2.5    |            |
| 2: CNN            |    -/2.5    |            | 
| <b>Total          |    -/5      |     </b>   |
