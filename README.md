# getting-and-cleaning-data-project

#Instructions#

* Process relies on R programming language with library `reshape2` 

* Download and unzip data from the following address:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

* Note: unzipped data from this file is assumed to be in the working directory

* execute `run_analysis.R`

The script will create a tidy dataset (`tidyDataset-AverageValues.txt` as described in CodeBook.md and place it in the same directory.

#Pseudo Code for Data Transformation#

    For train and test subdirectories:
      o read ./<directory>/X_<directory>.txt into data frame
      o append (via cbind) columns for subject and activity from 
        ./<directory>/subject_<directory>.txt 
        and ./<directory>/y_<directory>.txt
      o concatenate results to master data frame
      
    Read column names defined in features.txt; note column positions.
    Reduce data frame to appropriate columns (only those that include titles with mean() and std()) 
    Adjust activity column to reflect character description rather than number.
    Write reduced data frame to a .csv file.
    
    Summarize reduced data frame by the following 
      "class" variables: Activity and subject.
      compute average for all columns using the melt and dcast functions
      and place results in a summary data frame (tidy data set).
    Write summary data frame to .txt file.

#R Code#

    if (exists("masterData")) {remove(masterData)}
        
    for (directory in c("test","train")) {
      # read observation data
      filename <- paste("X_",directory,".txt",sep="")
      fileref<-paste(directory,filename,sep="/")
      observationData <- read.csv(fileref,header=FALSE,sep="")
      # read and append subject column
      filename <- paste("subject_",directory,".txt",sep="")
      fileref<-paste(directory,filename,sep="/")
      subjectData <- read.csv(fileref,header=FALSE,sep="")
      observationData <- cbind(observationData,subjectData)
      # read and append activity column
      filename <- paste("y_",directory,".txt",sep="")
      fileref<-paste(directory,filename,sep="/")
      activityData <- read.csv(fileref,header=FALSE,sep="")
      observationData <- cbind(observationData,activityData)
      # concatenate this data to all data.
      if (!exists("masterData")) {
        masterData <- observationData
      } else {
        masterData <- rbind(masterData, observationData)
      }
    }
    
    # Adjust activity column to reflect character description rather than number.
    activityColumn <- ncol(masterData)
    
    # determine which columns to retain:
    #   Those titled "*-mean(*" or "*-std(*" and the last 2
    
    fileref<-"features.txt"
    columnInfo <- read.csv(fileref,header=FALSE,sep="")
    columnInfo <- columnInfo[grep("-(?:mean|std)[(]",columnInfo[[2]],ignore.case=TRUE,value=FALSE,perl=TRUE),]
    
    # append info for the subject and activity column
    columnInfo[,2] <- sapply(columnInfo[,2],as.character)
    columnInfo <- rbind(columnInfo, c(activityColumn-1,"Subject"))
    columnInfo <- rbind(columnInfo, c(activityColumn,"Activity"))
    columnInfo[[1]] <- as.numeric(columnInfo[[1]])
    
    # condense masterData to include only columns documented in columnInfo.
    retainOnlyTheseColumns <- columnInfo[[1]]
    masterData <- masterData[,retainOnlyTheseColumns]
    # and assign the appropriate names to remaining column of masterData
    columnNames <- columnInfo[[2]]
    names(masterData) <- columnNames
    
    # Adjust activity column to reflect character description rather than number.
    activityColumn <- ncol(masterData)
    masterData[[activityColumn]][masterData[[activityColumn]]==1] <- "WALKING"
    masterData[[activityColumn]][masterData[[activityColumn]]==2] <- "WALKING_UPSTAIRS"
    masterData[[activityColumn]][masterData[[activityColumn]]==3] <- "WALKING_DOWNSTAIRS"
    masterData[[activityColumn]][masterData[[activityColumn]]==4] <- "SITTING"
    masterData[[activityColumn]][masterData[[activityColumn]]==5] <- "STANDING"
    masterData[[activityColumn]][masterData[[activityColumn]]==6] <- "LAYING"
    
    # write the file with a reduced number of columns
    fileref<-"fewColumns.csv"
    if (file.exists(fileref)) {
      file.remove(fileref)
    }
    write.table(masterData,file=fileref,col.names=TRUE,sep=",",row.names=FALSE)
    
    # prepare a "tidy" data frame that is aggregated by subject and activity
    # and contains the average value for all other columns
    
    require(reshape2)
    df_melt <- melt(masterData, id=c("Subject","Activity"))
    tidyDf  <- dcast(df_melt, Subject + Activity ~ variable, mean)
    fileref<-"tidyDataset-AverageValues.txt"
    if (file.exists(fileref)) {
      file.remove(fileref)
    }
    write.table(tidyDf,file=fileref,col.names=TRUE,sep=",",row.names=FALSE)
    
