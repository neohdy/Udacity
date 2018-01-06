# **Traffic Sign Recognition** 

by Neo He

## Writeup


**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report

[//]: # (Image References)
[image1]: ./Distribution.jpg "Distribution"
[image2]: ./rotation.jpg "rotation"
[image3]: ./architecture.jpg "architecture"
[image4]: ./Accuracy_curve_LeNetnew_20ep.jpg "curve"
[image5]: ./Testresult.jpg "result"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

here is my [project code]

### Data Set Summary & Exploration

The data set consists of tens of thousands 32x32 pictures of German traffic signs. The original size of the data set is shown below:
* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32 x 32
* The number of unique classes/labels in the data set is 43
Here is an exploratory visualization of the data set. It is a bar chart showing how the data...

![alt text][image1]

In order to make the data more diverse, some pre-process methods are applied. Firstly, for the aim of eliminate the influence of  color, the pictures are all transformed into gray scale from RGB scale. Then the normalization process is used by (pixel - 128)/ 128. And finally, some more data are added into the training set which are randomly rotated for some degree. 
After the process, the new size of the training data is 35164 and the shape of a image is 32x32x1.
Pictures compared the original with the processed one are shown below.

![alt text][image2]

### Design and Test a Model Architecture
The architecture of the model is modified refered to the *'Traffic Sign Recognition with Multi-Scale Convolutional Networks'* by Pierre Semanet and Yann LeCun, which has the architecture as below.
![alt text][image3]

The final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x6 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  valid padding, outputs 14x14x6 				|
| Convolution 5x5	    | 1x1 stride, valid padding, outputs 10x10x16      									|
| RELU           |   |
| Max pooling | 2x2 stride, valid padding, outputs 5x5x16|
| Flatten | output 400|
|Convolution 5x5 | 1x1 stride, valid padding, outputs 1x1x400|
|RELU| |
| Flatten | output 400|
|Layer2flat | output 800 |
|dropout| |
| Fully connected		| output 43|

### Training process

To train the model, I used the Adam optimizer and the batch size is 128. Epoches is 20.
The change of the loss and accuracy of the training and validation data are shown below.
![alt text][image4]

### Results and Tuning process
Firstly, the pre-process is tested by compare the pre-processed data and the original data. The result is shown below.The final training and validation accuracy of each one is:

|          		|     training accuracy  					| validation accuracy |
|:---------------------:|:---------------------------------------------:|:----:| 
|      Processed data     		| 0.868	| 
| Original data    	|   0.927 |


As can be seen, using the same model and epoches, the processed data can have a much better performance which has a faster convergence speed and can achieve higher accuracy. This means that the pre-process does play an important role of the deep learning method. 

As for the learning rate, it draws my attention that if the learning rate is too large, for example 0.01, then the accuracy will decrease dramaticly to 0.054 and remain around 0.05 while the learning is changed to 0.001, the accuracy will return to the normal value. This shows that the learning rate is quite important for the performance of the model. 

In traditional ConvNets, the output of the last stage is fed to a classifier. In the present work the outputs of all the stages are fed to the classifier. This allows the classifier to use, not just high-level features, which tend to be global, invariant, but with little precise details, but also pooled low- level features, which tend to be more local, less invariant, and more accurately encode local motifs.


### Test the model on new images

The results are shown below.
![alt text][image5]


Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Stop Sign      		| Stop sign   									| 
| U-turn     			| U-turn 										|
| Yield					| Yield											|
| 100 km/h	      		| Bumpy Road					 				|
| Slippery Road			| Slippery Road      							|

The model was able to correctly guess 4 of the 5 traffic signs, which gives an accuracy of 80%. This compares favorably to the accuracy on the test set of ...


For the first image, the model is relatively sure that this is a stop sign (probability of 0.6), and the image does contain a stop sign. The top five soft max probabilities were


