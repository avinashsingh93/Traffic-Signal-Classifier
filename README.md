# **Traffic Sign Recognition** 



### This project takes some images as input and then predicts the label for those images.

---

**Build a Traffic Sign Recognition Project**


## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  



### Data Set Summary & Exploration

#### 1. Below is the basic summary of the data set.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is: 34799
* The size of the validation set is: 4410
* The size of test set is: 12630
* The shape of a traffic sign image is: (32x32x3)
* The number of unique classes/labels in the data set is: 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set:

1) Training Bar
![training bar](/output_images/training_bar.png)

2) Validation Bar
![validation bar](/output_images/validation_bar.png)

3) Test Bar
![test bar](/output_images/test_bar.png)


### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

My first step was to implement my model withou any preprocessing. When I train my model without any pre processing, i got 88% aaccuracy. In order to increase the accuracy i applied some of the  preprocessing techniques. Preprocessing techniques used by me includes 1) converting the image into grayscale and 2)normalizing the grayscale image.
I converted my image into grayscale in order to remove excess information which becomes quite confusing while training the model. Then i normalized the image as this also increases the performance of the model. before normalizing the image, the pixel intensities vary for all the image sets (training, valiadtion and test). Hence this process resulted in increase in performance of the same.

Below are the images after the preprocessing them:

![pre_processed_images](/output_images/preprocesed_images.png)


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| (32x32x1) grayscale image   							| 
| Convolution 5x5    	| 1x1 stride, VALID padding, outputs 28x28x6 	|
| RELU					|												|
| Dropout				|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x6 				|
| Convolution 5x5	    | 2x2 stride, VALID padding, outputs 10x10x16     									|
| RELU				|												|
| Dropout				|												|
| Max pooling           | 2x2 stride 5x5x16
| Flatten
| RELU				|												| 
| Fully connected		| Output = 120        									|
| RELU				|												| 
| Fully connected		| Output = 84        									|
| RELU				|												| 
| Dropout				|												|
| Fully connected		| Output = 43        									|
| Softmax				| 														|
 


#### 3. Methods while training the model.

I used Adam Optimizer technique with:
batch size=128
number of epochs=40 
learning rate=0.00098 and 'dropout=0.5
I used LeNet model with some additional techniques like max pooling, dropout  and RELU activation.

#### 4. Getting validation accuracy >=94%.

My final model results were:
=> training set accuracy of 99.7%
=> validation set accuracy of 94.7%
=> test set accuracy of 93.5%

The first step which i used was similar to LeNet Architecture. But by this i was getting validation accuracy aruoond 88%. Hence i used some preprocessing techniques which includes grayscaling the image and then normalizing the image. This led to increase in validation accuracy around 93%. But test accuracy was still around 90%. After i applied dropout technique, test accuracy increased to 93.5% and validation accuray was around 95%.

 

### Test a Model on New Images

Below are the  five German traffic signs that I found on the web:

![100_kmhr](/test_image_check/100_kmhr.png)
![bumpy_road](/test_image_check/12.png)
![animal_crossing](/test_image_check/6.png)
![work_in_progress](/test_image_check/image_2.png)
![50_kmhr](/test_image_check/image_4.png)

First image is of Speed limit (100km/h) which was difficult to classify as it was little tilted. Since there was very less space between two zeroes, there are high chances of getting wrong prediction for this image.

Second images is of Bumpy road. This image would become difficult if it is taken as a straigh line figure instead of of bumps on it. This would make it resemble more like General Caution image.

Third image is of Animal crossing the road. Recognizing this image is difficult as it has some characteristics of "Double Curve signal" image. If some of features are not in image, then it would make it more like Double Curve signal.

Fourth image is of Road work sign. Classifying this image might be difficult only when Human sign is little distorted. It would make it look like Animal crossing the road. 

Fifth image is of 50 kmh. This image might become diffiult to recognize when '5' is not much clear. This would make it look like any other speed like 60 kmhr or 30 kmhr.



#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Below are the results of correct prediction of my model on new images:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Bumpy road      		| Bumpy road   									| 
| Wild animals crossing | Wild animals crossing 						|
| Road Work				| Road Work										|
| 50 km/h	      		| 50 km/h					 					|

My model was able to guess above 4 images correctly but it was not able to correctly guess one image(100 km/hr).
It was predicitng it as 80 kmhr. This might be because the image was litle bit titlted. Although my model got an accuracy of 80% for the new test images.


