# Getting and Cleaning Data Course Project #

## Project ##
Creation of a Tidy Dataset

## Source Data Set ##

Source data are described at:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

Data required for this exercise were downloaded at the following link:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

A description of the data is provided at:

http://archive.ics.uci.edu/ml/machine-learning-databases/00240/UCI%20HAR%20Dataset.names

## Source Files ##

The following files were used to complete the assignment:

* `features.txt`, A list of 531 data items collected for each observation set
* `X_train.txt`, `X_test.txt`,  files of observation sets, 1 row per observation set
* `subject_train.txt`, `subject_test.txt`, files with 1 subject id per observation.  
* `y_train.txt`, `y_test.txt`, files with activity id per observation


## Variables ##

### Classification Variables ###

* subject_id (from `subject_train.txt` and `subject_test.txt`).  These ranged from 1 to 30.
* activity id (from `y_train.txt` and `y_test.txt`).  These were coded fields ranging from 1 to 6.  They were coded to represent WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, and LAYING

### Observation Variables ###
531 variables included in each row of `X_train.txt` and `X_test.txt`. Descriptive titles for each variable documented in features.txt.  Additional descriptive information included in a documentation file `features_info.txt`

## Transformations ##

* Training and test data sets were read into data frames
* Columns for classification variables (Activity and Subject) were appended
* Training and test data frames were concatenated.
* Columns which did not describe Activity, Subject or which were *not* documented to reference mean() or std() were removed
* Column names were defined as Activity, Subject or according to documentation in `features.txt`
* average values for all observational variables grouped by Classification Variables (Activity and Subject)
were computed and recorded in a tidy dataset (`tidyDataset-AverageValues.txt`).

