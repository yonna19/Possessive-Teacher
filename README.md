# Reversed Maximize Learning: Achieving Robust Anti-Distill Models

Yao Zhang, Yang Li, Yahao Hu, Tianfeng Wang, Zhisong Pan*, Man Chen, Jun Chen

In under review

## Abstract
The prevalence of knowledge distillation has caused a significant increase in privacy and intellectual property violations. Existing work faked multi-peak logits to confuse the student models, aiming to prevent infringements through knowledge distillation. However this may introduce noise into the training of anti-distill models inadvertently and decreased the performance. To tackle this issue, we propose a method named Reversed Maximize Learning to obtain a robust anti-distill model, referred to as possessive teacher. We reverse the distribution of the original model according to the sort of logits in it to disrupt the output of anti-distill model. Besides, a binary probability is set to decouple the target and non-target classes utilizing a ground truth mask, so that the possessive teachers can maintain or even surpass the capabilities of the original models. Exclusive experiments were conducted on various models, and the results certify the effectiveness of our method both in data-available and data-free circumstances.

## Overview 

* We investigate the issue how to train a more robust anti-distill model, and explain how non-target classes work during KD. We find that confusing student models with a multi-peak logits distribution will introduce noise into the training of the anti-distill teacher, so we aim to eliminate the discrepancy in non-target classes;
* We propose a simple yet effective method, called Reversed Maximize Learning, to train a robust anti-distil model, which has a comparable performance with original model and can disturb the training of student models;
* Extensive experiments were conducted on various distillation methods, including vanilla KD and data-free KD, to verify the effectiveness of the proposed method. We can obtain an anti-distill model with better performance than the previous method, which can still destroy the learning process of the potential stealer.


## Prerequisite
We use Pytorch 1.13.1, and CUDA 11.7. 

You can install the needed packages by
~~~
pip install -r requirements.txt
~~~

## Usage 


### Train teacher network

##### Step 1: Train a normal teacher

~~~
python train_scratch.py --save_path [param_path]
~~~

For example, normally train a ResNet18 on CIFAR-10  
~~~
python train_scratch.py --save_path exps/CIFAR10/baseline/resnet18
~~~

##### Step 2: Train a possessive teacher
~~~
python train_possessive.py --save_path [param_path]
~~~
 
For example, train a possessive ResNet18
~~~
python train_nasty.py --save_path exps/CIFAR10/kd_possessive_resnet18/possessive_resnet18
~~~

### Train student networks 

~~~
python train_kd.py --save_path [param_path]
~~~

For example, train a ResNet8 distilling from a possessive ResNet18 
~~~
python train_kd.py --save_path experiments/CIFAR10/kd_possessive_resnet18/resnet8
~~~


## Acknowledgement
* DFAD from [https://githubfast.com/VainF/Data-Free-Adversarial-Distillation]
* Nasty-teacher from [https://githubfast.com/VITA-Group/Nasty-Teacher]

