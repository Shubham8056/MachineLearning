# MachineLearning
# Prediction Assignment

# Background

# Using devices such as Jawbone Up, Nike FuelBand, and Fitbit it is now possible to collect a large amount of data about personal activity relatively inexpensively. These type of devices are part of the quantified self movement – a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. One thing that people regularly do is quantify how much of a particular activity they do, but they rarely quantify how well they do it. In this project, your goal will be to use data from accelerometers on the belt, forearm, arm, and dumbell of 6 participants. They were asked to perform barbell lifts correctly and incorrectly in 5 different ways. More information is available from the website here: http://web.archive.org/web/20161224072740/http:/groupware.les.inf.puc-rio.br/har (see the section on the Weight Lifting Exercise Dataset).

#Load all the libraries
> library(caret)

> library(randomForest)

#Load the train data set
> training <- read.csv("C:/Users/Rabindra/Downloads/pml-training.csv")

#Load the test data set
> testing <- read.csv("C:/Users/Rabindra/Downloads/pml-testing.csv")

> set.seed(1234)

#Remove all columns with NULL values
> training<-training[,colSums(is.na(training)) == 0] 

> testing<-testing[,colSums(is.na(testing)) == 0]

#Divide Training data and Test data
> inTrain <- createDataPartition(y=training$classe, p=0.7, list=FALSE)

> Training1 <- training[inTrain, ]

> Testing1 <- training[-inTrain, ]

#Create model on basis of significant parameters present in dataset.

> model <- randomForest(classe ~ yaw_belt + roll_forearm +roll_belt + magnet_dumbbell_z + pitch_belt +pitch_forearm + magnet_dumbbell_y + magnet_dumbbell_x + accel_belt_z +  magnet_belt_z + magnet_forearm_z , data=Training1, method="class")


> prediction <- predict(model, Testing1, type = "class")

> confusionMatrix(prediction, Testing1$classe)





Confusion Matrix and Statistics

          Reference         
             A    B    C    D    E
         A 1384    4    1    0    0
         B    0  932    4    0    2
         C    9    8  843    5    0
         D    2    5    7  797    2
         E    0    0    0    2  897

Overall Statistics
                                          
               Accuracy : 0.9896          
                 95% CI : (0.9863, 0.9922)
    No Information Rate : 0.2845          
    P-Value [Acc > NIR] : < 2.2e-16       
                                          
                  Kappa : 0.9868          
                                          
 Mcnemar's Test P-Value : NA              


Statistics by Class:

                     Class: A Class: B Class: C Class: D Class: E
          Sensitivity  0.9921   0.9821   0.9860   0.9913   0.9956
          Specificity  0.9986   0.9985   0.9946   0.9961   0.9995
          Pos Pred Value 0.9964   0.9936   0.9746   0.9803   0.9978
          Neg Pred Value 0.9969   0.9957   0.9970   0.9983   0.9990
          Prevalence     0.2845   0.1935   0.1743   0.1639   0.1837
          Detection Rate 0.2822   0.1900   0.1719   0.1625   0.1829
          Detection Prevalence 0.2832   0.1913   0.1764   0.1658   0.1833
          Balanced Accuracy 0.9953   0.9903   0.9903   0.9937   0.9975


Accuracy of Random Forest model is 98.96

#Final Prediction 

> result <- predict(model, testing,type="class")

>result


#Categorization on the basis of prediction

    1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 
    B  A  B  A  A  E  D  B  A  A  B  C  B  A  E  E  A  B  B  B 
    Levels: A B C D E




