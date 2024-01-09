# LULC Map Preparation using Random Forest Classifier
A machine learning classification model to classify image data.


# Executive Summary
Land Use Land Cover (LULC) map provides information on the Earth’s surface. Temporal LULC maps will help monitor dynamic changes in agricultural ecosystems, forest conversions, surface water
bodies, etc. These maps can be generated in unsupervised or supervised ways.


# Problem Statement
To prepare LULC map using Sentinel-2 VNIR bands.


# Process Overview
The process consists of three main steps:
1. Data Sourcing
2. Data Preparation
3. Model Training

## 1. Data Sourcing:
Sentinel-2 Surface Reflectance 2A data products are downloaded from the Copernicus open-access hub. Blue, Green, Red, Red-Edge, and NIR are the bands considered for the analysis.

## 2. Data Preparation:
Annotators created the labeled Sentinel-2 scenes to assist supervised classifiers using QGIS/ArcGIS software. The labeled dataset is created with polygon vector shapefiles with Sentinel-2 satellite imagery as a base map. Each polygon should be given two fields: an ‘ID’, and a 'Class'. The examples of different classes appearing in Sentinel-2 imagery are made as references for annotators in the annotation guide.

During the data preparation phase, the following steps were performed: <br/>
**Importing the shapefile:** The shapefile containing the spatial data was imported. <br/>
**Extracting class names:** All class names were extracted from the imported shapefile. <br/>
**Creating a class dictionary:** A dictionary was created to assign numerical labels to each class. <br/>
**Looping through training classes:** The code iterated through each training class and its associated polygons. <br/>
**Reading image raster and extracting values:** The image raster was read, and the pixel values were extracted for the training polygons. <br/>
**Assigning outputs:** The extracted pixel values were assigned as the input features (x), and the corresponding class labels were assigned as the target variable (y). 

## 3. Model Training:
The model training phase involved the following steps: <br/>
**Test-train split:** The data was split into a 20% test set and a remaining training set. <br/>
**Calculating class weights:** Class weights were calculated to account for imbalanced training samples. <br/>
**Hyperparameter tuning:** The model's hyperparameters were adjusted to optimize performance. <br/>
**Training the model:** The final step involved training the model using the RandomForestClassifier algorithm. Random forest shows better classification accuracy in comparison to other machine learning algorithms from the literature study.

# How it works...
## Dataset Details
To train the model, the chosen region of interest was Ghaziabad, India. Two files were utilized in the training process:<br/>
**Raster data:** <br/>
![image](https://github.com/aishwarya-10/random_forest_classification/assets/48954230/62536e5e-ba10-4049-821d-dd296c4023c0) <br/>

**Shapefile:** <br/>
![image](https://github.com/aishwarya-10/random_forest_classification/assets/48954230/ce87d1c5-a012-457a-be88-418ccf0de4ad)

A total of six classes were identified for classification within the training data:
1. Barren
2. Grass
3. Shadow
4. Urban
5. Vegetation
6. Water

## Random Forest Algorithm
•	Random forest is a supervised learning algorithm that uses multiple decision trees for classification and regression. It works on the concept of using multiple decision trees.<br/>
•	From training sets, a random subset is taken, and individual decision trees are constructed. Each decision tree gives a vote for a class. The class with majority voting will be assigned to the pixel.<br/>
•	This method is popular as it shows less overfitting because the model is trained independently on subsets of training data.<br/>

The Random Forest algorithm achieved an accuracy of 0.89 in the classification task. The confusion matrix below provides a detailed breakdown of the algorithm's performance on the test data: <br/>

<div align="center">
    <img width="500" src="https://github.com/aishwarya-10/random_forest_classification/assets/48954230/f7a14089-ffa8-4ef4-bfe4-0bdb5ad1265c"> <br/>
    Figure 1. Confusion Matrix 
</div>

The algorithm demonstrated high precision and recall for classes barren, grass, urban, and vegetation, with values ranging from 0.79 to 0.95.<br/>
For class “water”, the algorithm displayed a relatively high recall of 0.94, indicating a good ability to identify instances of this class. However, the precision and F1-score were lower at 0.72 and 0.82,
respectively. This suggests that while the algorithm correctly identified most instances of the “water” class, it also produced a notable number of false positives (mainly “barren” and “urban”). Here is a
breakdown of the contribution of each of the bands in the classification of each class: <br/>

<p align="center"> Table. Contribution of each band in the classification of each class </p>
<img src="https://github.com/aishwarya-10/random_forest_classification/assets/48954230/50baa43c-5bd7-4f10-a490-f4f92749ee3b"> <br/>

Finally, presented below is a side-by-side plotted image, allowing for a visual comparison between the original image and the output generated using the algorithm. <br/>

![image](https://github.com/aishwarya-10/random_forest_classification/assets/48954230/caeb6acd-d52d-46a1-ac8d-8c1786f024ff)
<p align="center"> Figure 2. Comparison of the original image and classified image </p>





