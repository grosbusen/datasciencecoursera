#Getting and Cleaning of Data Course Project
The purpose of this project is to demonstrate your ability to collect, work with, and clean a data set. The goal is to prepare tidy data that can be used for later analysis. 

Here are the things that you can find in this repository
  1. codebook.md: that describes the variables, the data, and any transformations or work that you performed to clean up the data
  2. TidyDataSet.txt: a tidy data set
  3. run_analysis.R: script that perform analysis and create the tidy data set
  4. readme.md, which is what uare reading now
  
#Code Walkthrough
The first step you need to do is to install.packages like dplyr and tidyr as the script needs it, however for simplicity sake and compatibility issue, it is not in the script attached here, so please load all the require library on your own.
Please also set up working directory at your own as each working directory is different
The following the walkthrough of the attached scripts
  1. Download the file and unzip the the file to the location that we want
  ```R
  locationUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
  if (!file.exists("./data")){
    dir.create("./data")
  }
  download.file(locationUrl, destfile = "./data/Assignment.zip")

  #unzip dataset to directory
  unzip(zipfile="./data/Assignment.zip", exdir = "./data")  
  ```
  2. Read all the file from the train and test folder and assign a descriptive variable matching the file name for easy identification. reading the text files use read.table and stringsAsFactors is set to FALSE
  3. Assign a descriptive column name for the subject data (SubjectID) and activity data(ActivityID)
  4. Combine all the data from test and train folder to a single data frame called mydf
  5. Use grepl to extract the mean and standard deviation measurement from all the measurements. In this case, mean measurement like MeanFreq and mean related angle are included in this version.
  Just a reminder, that there is no right or wrong to which set of mean that can only be extracted in this data frame.
  6. The value return from the grepl is the indices of all measurement that have mean and standard deviation. Assign a new variable base on the indices of measuremnt of mean and standard deviation
  7. Apply a appropriate labels to the data set measurement with descriptive variable names from features data frame. This steps add a new column, ActivityDescription to accompany ActivityID. Remove the ActivityID using select()
  8. Assign descriptive activity names by merging the data set with activities data frame
  9. Using aggregate to have a summary base on each subject and activity and measure the average of every measurement in the data frame base on the subject and activity
  10.Use write table to create a second independent tidy data set churn out from step 9

