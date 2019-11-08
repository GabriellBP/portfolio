---
layout: post
title: Effectiveness Analysis with R
description: >
  A overview about effectiveness analysis with R.
image: /assets/img/blog/data-science/Confusion-matrix.png
noindex: true
---

Analyzing the effectiveness of an algorithm is very important in deciding which model to use. For that, we have some 
measure options like accuracy, precision, recall, F-measure among others. Here, I’ll explain a little about precision, recall,
and F-measure, presenting an implementation of them in R.

Above is an image showing the confusion matrix and its fields, look and read ir before you continue reading.

Just to now:
*   **True Positive (TP):** The correctly predicted positive values. E.g. if a patient has diseases, and the model tells you the same thing.
*   **True Negative (TN):** The correctly predicted negative values. E.g. if a patient has no diseases, and the model tells you the same thing. 
*   **False Positive (FP):** The predicted value is yes, but the actual value is no. E.g. if a patient has no diseases, and the model tells you that the patient have diseases. 
*   **False Negative (FN):** The predicted value is no, but the actual value is yes. E.g. if a patient has diseases, and the model tells you that the patient have no diseases. 

## Precision
In short terms, precision is the fraction of relevant instances among the retrieved instances. In other words, precision
talks about how precise your model is, out of those predicted positive, how many of them are actual positive, it's the ratio
of correctly predicted positive observations to the total predicted positive observations. 

It's good to use, when you wanna determine when the costs of false positive is high.

The formula:
![](https://miro.medium.com/max/444/1*C3ctNdO0mde9fa1PFsCVqA.png)

In R, we can calculate the precision measure in this way:

~~~R
# Precision
precision <- function(tp, fp){
  
  precision <- tp/(tp+fp)
  
  return(precision)
}
~~~

## Recall
Being fast, recall is the fraction of the total amount of relevant instances that were actually retrieved. I mean, recall
calculates how many of the Actual Positives our model capture through labeling it as Positive, it's the ratio of correctly 
predicted positive observations to the all observations in actual positive (yes) class.

We wanna use it to select our best model when there is a high cost associated with False Negative, e.g. in fraud detection 
or sick patient detection.

The formula:
![](https://miro.medium.com/max/418/1*dXkDleGhA-jjZmZ1BlYKXg.png)

In R, we can calculate the recall measure in this way:

~~~R
# Recall
recall <- function(tp, fn){
  
  recall <- tp/(tp+fn)
  
  return(recall)
}
~~~

## F-Measure
F-Measure function is the way to calculate the F1 Score, that's a way to measure the model's accuracy. F1 Score  is the 
weighted average of Precision and Recall and might be a better measure to use if we need to seek a balance between 
Precision and Recall, this score takes both false positives and false negatives into account. And it's more useful than 
accuracy, especially if you have an uneven class distribution (large number of Actual Negatives) - _Accuracy works best 
if false positives and false negatives have similar cost_.

F1 Score is needed when you want to seek a balance between Precision and Recall

The formula:
![](https://miro.medium.com/max/282/1*T6kVUKxG_Z4V5Fm1UXhEIw.png)

In R, we can calculate the F-Measure in this way:

~~~R
# F-measure
f_measure <- function(tp, fp, fn){
  
  f_measure <- (2*precision(tp,fp)*recall(tp,fn))/(recall(tp,fn) + precision(tp, fp))
  
  return(f_measure)
}
~~~

## Conclusion
So now we know that there're different types of measures, and each one is better in specific scenarios. Beyond, we have 
learned that's important to analyse the effectiveness of our models with different types of measurement, to know which model 
we will choose for each situation.

Below we have a function to calculate the three measures mentioned above:

~~~R
measures <- function(test, pred){
  
  true_positive <- 0
  true_negative <- 0
  false_positive <- 0
  false_negative <- 0
  
  for(i in 1:length(pred)){
    if(test[i] == TRUE && pred[i] == TRUE){
      true_positive <- true_positive + 1
    }else if(test[i] == FALSE && pred[i] == FALSE){
      true_negative <- true_negative + 1
    }else if(test[i] == FALSE && pred[i] == TRUE){
      false_negative <- false_negative + 1
    }else if(test[i] == TRUE && pred[i] == FALSE){
      false_positive <- false_positive + 1
    }
  }
  
  measures <- c(precision(true_positive,false_positive), 
                recall(true_positive,false_negative), 
                f_measure(true_positive,false_positive,false_negative))
  
  return(measures)
}
~~~

