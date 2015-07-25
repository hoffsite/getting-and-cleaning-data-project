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
* `y_train.txt`, `y_test.txt`, files with 1 activity id per observation


## Variables ##

### Classification Variables in provided data set ###

* subject_id (from `subject_train.txt` and `subject_test.txt`).  These ranged from 1 to 30.
* activity id (from `y_train.txt` and `y_test.txt`).  These were coded fields ranging from 1 to 6.  They were coded to represent WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, and LAYING

### Observation Variables in provided data set ###
531 variables included in each row of `X_train.txt` and `X_test.txt`. Descriptive titles for each variable documented in `features.txt`.  Additional descriptive information included in a documentation file `features_info.txt`

## Transformations ##

* Training and test data sets were read into data frames
* Columns for classification variables (Activity and Subject) were appended
* Training and test data frames were concatenated.
* Columns which did not describe Activity, Subject or which were *not* documented to reference mean() or std() were removed
* Column names were defined as Activity, Subject or according to documentation in `features.txt`
* Activity column was transformed from a number (1 to 6) to a character description (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING)
* average values for all observational variables grouped by Classification Variables (Activity and Subject)
were computed and recorded in a tidy dataset (`tidyDataset-AverageValues.txt`).

### Variables in tidyDataset-AverageValues.txt ###
    
    Subject (Number)
    Activity (Description)
    
    Variables below are average values for the referenced columns observed over all observations for matching Subject and Activity
    
    tBodyAcc-mean()-X
    tBodyAcc-mean()-Y
    tBodyAcc-mean()-Z
    tBodyAcc-std()-X
    tBodyAcc-std()-Y
    tBodyAcc-std()-Z
    tGravityAcc-mean()-X
    tGravityAcc-mean()-Y
    tGravityAcc-mean()-Z
    tGravityAcc-std()-X
    tGravityAcc-std()-Y
    tGravityAcc-std()-Z
    tBodyAccJerk-mean()-X
    tBodyAccJerk-mean()-Y
    tBodyAccJerk-mean()-Z
    tBodyAccJerk-std()-X
    tBodyAccJerk-std()-Y
    tBodyAccJerk-std()-Z
    tBodyGyro-mean()-X
    tBodyGyro-mean()-Y
    tBodyGyro-mean()-Z
    tBodyGyro-std()-X
    tBodyGyro-std()-Y
    tBodyGyro-std()-Z
    tBodyGyroJerk-mean()-X
    tBodyGyroJerk-mean()-Y
    tBodyGyroJerk-mean()-Z
    tBodyGyroJerk-std()-X
    tBodyGyroJerk-std()-Y
    tBodyGyroJerk-std()-Z
    tBodyAccMag-mean()
    tBodyAccMag-std()
    tGravityAccMag-mean()
    tGravityAccMag-std()
    tBodyAccJerkMag-mean()
    tBodyAccJerkMag-std()
    tBodyGyroMag-mean()
    tBodyGyroMag-std()
    tBodyGyroJerkMag-mean()
    tBodyGyroJerkMag-std()
    fBodyAcc-mean()-X
    fBodyAcc-mean()-Y
    fBodyAcc-mean()-Z
    fBodyAcc-std()-X
    fBodyAcc-std()-Y
    fBodyAcc-std()-Z
    fBodyAccJerk-mean()-X
    fBodyAccJerk-mean()-Y
    fBodyAccJerk-mean()-Z
    fBodyAccJerk-std()-X
    fBodyAccJerk-std()-Y
    fBodyAccJerk-std()-Z
    fBodyGyro-mean()-X
    fBodyGyro-mean()-Y
    fBodyGyro-mean()-Z
    fBodyGyro-std()-X
    fBodyGyro-std()-Y
    fBodyGyro-std()-Z
    fBodyAccMag-mean()
    fBodyAccMag-std()
    fBodyBodyAccJerkMag-mean()
    fBodyBodyAccJerkMag-std()
    fBodyBodyGyroMag-mean()
    fBodyBodyGyroMag-std()
    fBodyBodyGyroJerkMag-mean()
    fBodyBodyGyroJerkMag-std()
