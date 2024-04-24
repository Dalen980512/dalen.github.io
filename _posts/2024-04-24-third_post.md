# **Homework records**

This blog records the problems encountered in this assignment. There are three topics in this assignment: 1. Fingerprint recognition 2. Comparison of GPU and CPU 3. Training classification network and visualization results. For me, Question 1 is the most difficult. It requires designing a GUI and database, implementing fingerprint recognition, and measuring some indicators. Next is question 3. The main difficulty lies in visualizing the t-SNE diagram. Finally, question 2, the main problem solved is the CPU environment running problem of fastai. Below I will carefully record the problems encountered in this assignment.

## 1. Fingerprint recognition 

### Topic requirements.

You have been provided with a Jupyter notebook for fingerprint recognition available from https://github.com/lovellbrian/fingerprint . Design a GUI and template file/database which allows you to:

  -​ a. Enrol a fingerprint and associate a name. Store the template in a file or database

​	b. Compare a new fingerprint to the fingerprints in the gallery

​	c. Evaluate your system on a large number of fingerprints and adjust the threshold for good performance with low error rates

​	d. Produce a ROC curve showing error rates versus threshold

​	e. Estimate the false positive rate (false alarm rate) for a false negative rate of 1%.

You can fetch additional prints from http://bias.csr.unibo.it/fvc2000/download.asp.

### Question 1. Use of datasets:

I downloaded the data set from http://bias.csr.unibo.it/fvc2000/download.asp and selected DB1_B. The fingerprint after opening is as shown below, with the corresponding number. I don't quite understand the meaning of these numbers. Finally, I found on the official website that these fingerprints are 1xx_x.tif, where the number before '_' is the person's ID, and the number after '_' is the fingerprint ID corresponding to the person, that is to say, Each person corresponds to 8 fingerprints. From this perspective, I created a database that stores each person and their fingerprint information.

![1713936472737](C:\Users\Luffy\AppData\Roaming\Typora\typora-user-images\1713936472737.png)

​													Figure 1 DB1_B dataset

### Question 2.ROC curve:

The ROC curve is a measure of a classification problem, so I need to convert the fingerprint recognition task into a classification problem. Applied to the above data set, my idea is to treat a person as a category, and the 8 fingerprints as instances in the category. This turns the recognition problem into a classification problem. In addition, the fingerprint recognition score can be used as the confidence score of classification. With this, I got the results of the classification and got the ROC curve.

![1713936981273](C:\Users\Luffy\AppData\Roaming\Typora\typora-user-images\1713936981273.png)

​															Figure 2 Classification result diagram

## 2. Training classification network and visualizing results

### Topic requirements.

Write a Jupyter notebook to classify images with the same classes as the CIFAR10 dataset (i.e., airplane, automobile, bird, cat, deer, dog, frog, horse, ship, truck). Use Duck Duck Go to scrape sample images off the Web based on the fast.ai course example on birds. Design an appropriate multiclass loss function or describe which one was used. Analyse your data and results using tools such as t-SNE and Confusion matrices. Report on metrics such as classification accuracy and explain the methods used.

### Question 1.t-SNE

The t-SNE graph is a visualization method that compresses high-dimensional features onto a 2D graph. How to obtain the high-dimensional features of each sample is a difficult point. Thanks to the hook method in fastai, the output of a certain module of the model can be used to obtain the feature value in the form of a hook. From this, I used hooks to obtain the input features of the classification head as high-dimensional features of the t-SNE graph for the sample images in each verification set. After obtaining the high-dimensional features in this way, the label information corresponding to the sample is obtained to obtain the final t-SNE graph.



![1713937472458](C:\Users\Luffy\AppData\Roaming\Typora\typora-user-images\1713937472458.png)

Figure 3 t-SNE

## 3. Comparison of GPU and CPU

### Topic requirements.

This question is a brief exploration of running a Deep Learning notebook using a GPU or CPU. As far as I know, this is the first time this Development Container method has been used for teaching. It has taken me about 6 months to get this set up, so I hope you enjoy it. This task is mostly an exercise in getting your own devcontainer up and running on our 78-336 Lab machines and possibly also on your home machine or laptop. It is a hands-on exercise. Tutors will help you, so ask them for assistance. Get your machine set up for containers following my AI blog post at:https://lovellbrian.github.io/2023/10/02/BYODImage.html. Follow my blog instructions to first set up a CPU learning environment and then change this to a GPU deep learning environment running on Linux Ubuntu 22.04. Time the learning loop in the notebook using the CPU and you will find this often takes many minutes. Then we will try it using the GPU which will take seconds. For this exercise, figure out how to change the batch size in fastai. Google is your friend. The default value is 64.

(a) Try batch size values of 16, 32, 64, 128, and 256 on the GPU and determine which is fastest.

(b) Determine the maximum speedup of the GPU over the CPU.

(c) Show graphs on GPU activity using nvtop as described in the blog. Explain what you observe and any issues you encountered.

### Question 1.CPU environment configuration

Since fastai uses the GPU environment for experiments by default, when configuring the CPU environment, when running the original code directly, there will be some code base conflicts and errors. Specifically, changes to the original spaCy library caused compilation errors. Subsequent solution: Reinstalled the updated cpu container environment, used the test code again, success!
