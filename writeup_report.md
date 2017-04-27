#**Behavioral Cloning** 

**Behavioral Cloning Project**

[//]: # (Image References)

[image1]: ./images/Visualization.jpg "Normal Image"
[image2]: ./images/cropped.jpg "Cropped Image"
[image3]: ./images/recovery1.jpg "Recovery Image"
[image4]: ./images/recovery2.jpg "Recovery Image"
[image5]: ./images/recovery3.jpg "Recovery Image"

---
###Files Submitted & Code Quality

####1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* writeup_report.md or writeup_report.pdf summarizing the results

####2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track 1 for 2 complete laps.
The model (clonef.ipynb) uses only center camera images.
```sh
python drive.py model.h5
```

####3. Submission code 

The clonef.ipynb file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

###Model Architecture and Training Strategy
The model uses center camera images and steering angle as training images and labels respectively to learn.

####1. An appropriate model architecture has been employed

Model starts with normalization (keras lambda) of the 160, 320, 3 with 5x5 filter sizes with depth varying from 24 and 64 and 2x2 stride.

The model includes RELU layers to introduce nonlinearity.

####2. Attempts to reduce overfitting in the model

The model contains dropout layers in order to reduce overfitting.

The model was trained and validated on udacity provided data and data produced from simulator. Used simulator to run 2 laps with recovery simulation.

different data sets to ensure that the model was not overfitting (code line 10-16). The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

####3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually.

####4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I used a combination of center lane driving, recovering from the left and right sides of the road.

For details about how I created the training data, see the next section. 

###Model Architecture and Training Strategy

####1. Solution Design Approach

My first step was to use a convolution neural network model similar to the image classification. I thought this model might be appropriate because eventually a video is a series of images and each image has a signature and a steering angle as a label.

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. 

I started by runnig the model on the data I generated form simulator and found out that it is not enough and then added Udacity data and merged the driving_log.csv. Even after that my car was running into the woods/water. I then realized that I need to simluate some recovery data, where I drove the car to the edges and then corrected it from there after starting the recording, which really helped me get to the end state.

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

####2. Final Model Architecture

Model starts with normalization (keras lambda) of the 160, 320, 3  and cropping the image (70 pixels from the top and 25 from bottom) with 5x5 filter sizes with depth varying from 24 and 64 and 2x2 stride.


The model includes RELU layers to introduce nonlinearity.

####3. Creation of the Training Set & Training Process

To capture good driving behavior, I first recorded two laps on track one using center lane driving. Here is an example image of center lane driving:

![alt text][image1]

I then recorded the vehicle recovering from the left side and right sides of the road back to center so that the vehicle would learn tp recover.
These images show what a recovery looks like -

![alt text][image3]
![alt text][image4]
![alt text][image5]

I finally randomly shuffled the data set and put 20% of the data into a validation set. 
As it was taking 3 hours for 1 EPOCH, I tried autonomous mode with 1 EPOCH which sufficed.

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. I used an adam optimizer so that manually training the learning rate wasn't necessary.
