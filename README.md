# Codecademy's Forest Cover Classification (Portfolio Project)

This repository contains my solution to the forest cover classification project, which is the final portfolio project in Codecademy's course "Build Deep Learning Models with TensorFlow".

The Data was provided from Codecademy on geological aspects of the areas studied (obtained from the US Geological Survey and US Forest Service (USFS)), one observation describing 30x30 meter cell of forest. Labelling was determined from the USFS Region 2 Resource Information System data. 

Covertypes (Classes): 
- Spruce/Fir
- Lodgepole Pine
- Ponderosa Pine
- Cottonwood/Willow
- Aspen
- Douglas-fir
- Krummholz

581012 observations were provided with 54 features. 

____________ 

### EDA

This dataset was already cleaned, containing no null-values or artifacts.

There were 10 continuous features provided: 
- Elevation
- Aspect
- Slope
- Horizontal_Distance_To_Hydrology
- Vertical_Distance_To_Hydrology
- Horizontal_Distance_To_Roadways
- Hillshade_9am
- Hillshade_Noon
- Hillshade_3pm
- Horizontal_Distance_To_Fire_Points

Figure 1 shows the distribution of these 10 features in a random sample of 1000 observations of the data provided. The only feature that appears to distinguish the features somewhat on its own seems to be elevation with cover type 7 and type 1 being mostly found at higher elevation and cover type 3 at lower elevation. 

<p align="center"><img src="/visuals/pairplot_1.png"></p>  
<p align="center"><i>Figure 1. Pairplot of continuous features.</i></p> 

There were 2 categorical features, wilderness type and soil type. The data was presented in an already dummified form with 4 wilderness types and 40 soil types as seperate columns. Unfortunately no details about the wilderness and soil types were provided with the dataset. 

Figure 2 shows the distribution of different wilderness types among the 7 classes of forest covers. Interesting findings include, that all areas of forest cover type 4 are of wilderness type 4 while for example forest cover type 6 is almost evenly split between wilderness types 3 and 4. 

<p align="center"><img src="/visuals/wilderness_heatmap.png"></p>  
<p align="center"><i>Figure 2. Heatmap of wilderness types vs forest cover classes.</i></p> 

In figure 3 one can see the occurences of different soil types in the classes of forest covers. Again the classes vary substantially, with for example forest cover type 6 having soil type 10 in 51% of cases, while cover type 7 mostly appearing in combination with soil types 38, 39 and 40.

<p align="center"><img src="/visuals/soiltype_heatmap.png"></p>  
<p align="center"><i>Figure 3. Heatmap of soil types vs forest cover classes.</i></p>


#### Class imbalance

The 7 types of forest covers were heavily imbalanced with class 1 and 2 being the majority, distribution of classes is shown in figure 4. 

<p align="center"><img src="/visuals/class_imbalance.png"></p>  
<p align="center"><i>Figure 4. Distribution of classes.</i></p>

____________ 

### Preprocessing

A stratified train-test-split was performed, leaving out 20% of the data for the test-set. All predictors were used in standardized form. 

____________

### Modelling

Model architecture and hyperparameters were iterated over several times. Best results were obtained by a model with the architecture shown in figure 5. All hidden layers used ReLu, with the output layer's activation function being set to softmax. The loss-function was CategoricalCrossentropy and the optimizer Adam with a learning rate of 0.05. 

Fitting was performed with 50 epochs, a batch size of 512 and a validation split of 0.3. 
Train and validation loss are shown in figure 6.

<p align="center"><img src="/visuals/model_architecture.png"></p>  
<p align="center"><i>Figure 5. Model architecture.</i></p>

<p align="center"><img src="/visuals/loss_curve.png"></p>  
<p align="center"><i>Figure 6. Train and validation loss.</i></p>

____________

### Model Evaluation

On the test set the model scored an overall accuracy of 0.91. 

The confusion matrix standardized per true class can be seen in figure 7. Detailled scores for all classes are shown in the classfication report in figure 8.

<p align="center"><img src="/visuals/conf_matrix_plot.png"></p>  
<p align="center"><i>Figure 7. Confusion Matrix standardized by true class.</i></p>

<p align="center"><img src="/visuals/classification_report.png"></p>  
<p align="center"><i>Figure 8. Classification report.</i></p>


_____________

### Conclusion

From the features provided the type of forest cover can be predicted with an overall accuracy of 0.91. F1-Scores were lower for the two classes with the least observations, as was expected.

_____________

### Packages used
- pandas
- numpy
- seaborn
- matplotlib
- scikit-learn
- tensorflow


____________

### Lessons learned

It is surprisingly easy to create <i>a</i> neural network. Tuning it to get the best result possible is quite a challenge. As this was the first neural net I build on my own I am quite happy with the result, but also realized how much functionality there still is to discover in tensorflow. 
