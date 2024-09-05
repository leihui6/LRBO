# Look at Robot Base Once: Hand-Eye Calibration

Welcome to our project: Look at Robot Base (**LRBO**): Hand-eye Calibration.

Our idea can be applied for eye-in-hand and eye-to-hand calibration.

Our proposed method has **THREE** features:

1. *[**EASY**]* For both eye-in-hand and eye-to-hand calibration, it doesn't require any additional calibration objects (**No calibration objects**), such as a chessboard or something like that. 
2. Hand-eye calibration can be done with **only 3D point clouds**.
3. *[**FAST**]* The processing time could be fast (**<1 sec**) and the result is as accurate as other _3D vision-based methods_.

Overall, it is a **Fully Automatic** robot hand-eye calibration based on 3D vision (point cloud).

## Requirement

The overall requirement is as follows(Please install them following the official guideline):

- [PRADATOR](https://github.com/prs-eth/OverlapPredator): a 3D registration for low-overlap point clouds.
- [PVRCNN/PVRCNN++](https://github.com/open-mmlab/OpenPCDet): a 3D detection module for the robot base detection.
- The utilization for both above can be seen [here](./implementation/).

However, to utilize our solution in our project quickly, [here](./implementation/) contains the guideline where the performance can not be guaranteed but in simple cases, it should be working.

To be honest, the above libraries are generally not 'must required' if you look at the pipeline as shown below. The goal is to find the orientation and direction of the robot base in view of the camera (3D camera), so that we can estimate the transformation between the robot base and the camera directly and easily. To be honest, the above libraries are generally not 'must required' if you look at the pipeline as shown below. The goal is to find the orientation and direction of the robot base in view of the camera (3D camera), so that we can estimate the transformation between the robot base and the camera directly and easily. The other transformation could be solved by the classical forward kinetic model.


## Abstract

Hand-eye calibration is a fundamental task in vision-based robotic systems, referring to the calculation of the relative transformation between the camera and the robotic end-effector. It has been studied for many years. However, most methods still rely on external markers or even human assistance. This paper proposes a one-click and fully automatic hand-eye calibration method using 3D point clouds obtained from a 3D camera. Our proposed hand-eye calibration is performed much faster than conventional methods. This is achieved by the learning-based detection and registration of the robot base. In addition, the calibration is performed automatically using only one native calibration object, the robot base, which simplifies the process. Our proposed method is tested for repeatability and accuracy through a series of experiments.

## Pipeline

The pipeline for our proposed method is shown below (will be published soon), where eye-in-hand calibration is taken as an example because it is more complex compared to eye-to-hand calibration. The estimation of the transformation matrix between the camera and the robot base is a common problem for them.

<img src="./figs/pipeline.png" style="display: block; margin: 0 auto"/> 

The dataset generation for the robot base is elaborated in paper.

### Detection of Robot Base

Here we captured more than a series of point clouds from a [3D camera](https://github.com/leihui6/PMD_Camera). The raw point clouds are green and the Regions of Interest (ROIs) are blue (they are the same size, so they might be a bit hard to see :).

<img src="./figs/Raw_ROI.gif" width="20%" style="display: block; margin: 0 auto"/>  

### Registration of Robot Base

These ROIs, extracted from raw point clouds, are aligned with a model of the robot base (which is actually a point cloud as well), the registration result is shown below.

<img src="./figs/Raw_Model.gif" width="20%" style="display: block; margin: 0 auto"/> 

### Hand-eye Calibration

We can perform a hand-eye calibration with only a single point cloud. Therefore, we executed hundreds of calibrations (**eye-in-hand calibration**) during each data acquisition. The result is shown below, where the camera image is displayed close to the end-effector.

<img  src="./figs/workflow.gif" width="100%" /> 

### Video

Video and tutorial coming soon.

## Repeatability Experiment

By measuring the variability in the results, repeatability experiments can provide insight into the stability and robustness of the calibration method and ensure that the results are not merely due to random fluctuations. Therefore, more than 200 hand-eye calibrations were conducted in 300 sec (**surprise**?!). The results are shown below.

<img src="./figs/normRandT8.png" width="80%" style="display: block; margin: 0 auto"/> 

## Accuracy Experiment

Two types of testing are performed, called static testing and dynamic testing. Static testing is considered the ground truth.

| Method 	|    Position error (mm)    	| Rotation error (deg) 	| Runtime 	|  Camera Type 	|
|:------:	|:-------------------------:	|:--------------------:	|:-------:	|:------------:	|
|  Ours  	| **X**: 1.874 **Y**:1.092 **Z**: 0.303 	|         0.391        	|   1.5 + 5 (move)   	| ToF   Camera 	|
|  Ours  	| **X**: 1.159 **Y**:0.697 **Z**: 1.025 	|         0.994        	|  <1 + 5 (move)   	| Structured of Light   Camera 	|

## Implement Details

**[PREDATOR](https://github.com/prs-eth/OverlapPredator)**, a learning-based point cloud registration framework is applied in our project. In addition, the **[PV-RCNN++](https://github.com/open-mmlab/OpenPCDet)** as a 3D detection module to provide a rough location of the robot base is employed in our method. According to the evaluation result and experiments, their performance is excellent compared with other conventional registration methods (more details in the paper).

We here utilized real-world data to train these framework. The trained model in terms of PREDATOR and PV-RCNN++ can be downloaded as follows: 
- [Detection/Trained model](https://1drv.ms/u/s!AnRiouA_fmTVh6UpNm4gtWq02GF8JA): This model can be used for UR3e and UR5e robot base detection task
- [Registration/Trained model](https://1drv.ms/u/s!AnRiouA_fmTVh6UnauE3yxdVcgU5qQ): This model can be used for robot base registration. A model of robot base can be obtained from [Here](./dataset/readme.md).

## Papers

If you found it is helpful, please cite:

``` 
 @article{Li_Yang_Wang_Zhang_2024b, 
 title={Automatic robot hand-eye calibration enabled by learning-based 3D vision}, 
 volume={110}, 
 DOI={10.1007/s10846-024-02166-4}, 
 number={3}, 
 journal={Journal of Intelligent & Robotic Systems}, 
 author={Li, Leihui and Yang, Xingyu and Wang, Riwei and Zhang, Xuping}, 
 year={2024}, 
 month={Sep}, 
 pages={1–23} }

```

## Contribution

This project is maintained by @[Leihui Li](leihui$$$mpe.au.dk), please feel free to contact me if any questions.
