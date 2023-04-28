# SurgicalToolsSegmentation

AML Course - Assignment 2

A comparison between FasterRCNN and YOLOv8 in segmentation

## Dataset preperation

[m2cai16-tool-locations](http://ai.stanford.edu/~syyeung/resources/m2cai16-tool-locations.zip)

The m2cai16-tool-locations dataset has 210 images m2cai16-tool dataset. The dataset has 7 different types of surgical instruments.

![image](https://user-images.githubusercontent.com/94979970/229603941-36d19b1d-54c3-42aa-bf73-78c689fab954.png)

The images are annotated using Roboflow platform

After the annotation, the images are preprocessed to have the same size.

Then, some additional augmentation is applied on the image to generate additional image with different conditions (brightness and noise levels)

![image](https://user-images.githubusercontent.com/94979970/235088072-ff005275-7a5c-47ac-b39f-f268391c34d0.png)


Finally, we got a 532 annotated images divided into train, validation, and test as it shown below:

![image](https://user-images.githubusercontent.com/94979970/235087963-4ef3eb30-8097-4070-8755-70614d7fbd7d.png)

[Link to the annotated data](https://app.roboflow.com/amlcourse/surgical-tools-detection-tjnkm/1)


## Train FastRCNN model using Detectron2 on our Dataset

The generated dataset is exported in ***COCO Format***. A set of lines will be generated:

    !pip install roboflow

    from roboflow import Roboflow
    rf = Roboflow(api_key="***********")
    project = rf.workspace("*****").project("**************")
    dataset = project.version(*).download("coco")


[the project colab file for Faster RCNN](https://github.com/KaramAlmaghout/SurgicalToolsSegmentation/blob/main/AML_Assignment2_FasterRCNN.ipynb) 


### Results

![image](https://user-images.githubusercontent.com/94979970/235088718-c6966893-6dc6-4ccf-b92f-8b0a69f8bfc2.png)
![image](https://user-images.githubusercontent.com/94979970/235088744-fc25bd64-63cb-41ad-9b63-5de39853e8fe.png)
![image](https://user-images.githubusercontent.com/94979970/235088877-f980fc14-c7be-4de2-afb6-03a099317889.png)


Evaluation results for segm: 

|   AP   |  AP50  |  AP75  |  APs  |  APm  |  APl   |
|:------:|:------:|:------:|:-----:|:-----:|:------:|
| 42.015 | 49.995 | 45.096 |  nan  | 7.741 | 45.667 |

Per-category segm AP: 

| category       | AP     | category   | AP     | category   | AP     |
|:---------------|:-------|:-----------|:-------|:-----------|:-------|
| bag            | 62.824 | bipolar    | 38.713 |hook        | 46.733 |
| clipper        | 20.792 | grasper    | 53.636 |            |        |
| irrigator      | 71.407 | scissors   | 0.000  |            |        |



## Train YOLOv8 model on our Dataset

The generated dataset is exported in ***YOLOv8 Format***. A set of lines will be generated:

    !pip install roboflow
    
    from roboflow import Roboflow
    rf = Roboflow(api_key="="***********")
    project = rf.workspace("amlcourse").project("***********")
    dataset = project.version(*).download("yolov8")


[the project colab file for YOLOv8]()

### Results

![image](https://user-images.githubusercontent.com/94979970/235142408-13a88ba6-caa6-42a6-810b-6c883e9d8ccd.png)
![image](https://user-images.githubusercontent.com/94979970/235142426-ef272748-76c5-4342-9974-5a68e964c03d.png)


![image](https://user-images.githubusercontent.com/94979970/235142630-8173a67b-adc6-463e-aed2-30c7b746e66a.png)
![image](https://user-images.githubusercontent.com/94979970/235142706-f670c68a-1506-4de0-99e3-8e3c25bb2863.png)
![image](https://user-images.githubusercontent.com/94979970/235142975-f08dc070-244a-4f12-ab42-0ce475a45ae6.png)


