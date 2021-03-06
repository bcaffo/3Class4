R script called run_analysis.R

#Reading about the project at http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones , 

#I loaded the packages I thought I might use with a “just in case” attitude via the lower left pane: data.table, dplyr, ggplot2, git2r, lubridate, magrittr, plyr, readr, readxl, stringr, tidyr, writeexl.

#I downloaded the data set and saved it as HAR.zip from this website and read the ReadMe file

# I called in the pertinent Train and Test datasets by importing each separately using the import text function in the upper right pane. I used this website as a guide: https://thoughtfulbloke.wordpress.com/2015/09/09/getting-and-cleaning-the-assignment/ 	

> subject_test <- read.table("C:/Users/CA/Downloads/HAR/1/test/subject_test.txt", quote="\"", comment.char="")
> 
>   View(subject_test)
>   
> X_test <- read.table("C:/Users/CA/Downloads/HAR/1/test/X_test.txt", quote="\"", comment.char="")
> 
>   View(X_test)
>   
> y_test <- read.table("C:/Users/CA/Downloads/HAR/1/test/y_test.txt", quote="\"", comment.char="")
> 
>   View(y_test)
>   
> subject_train <- read.table("C:/Users/CA/Downloads/HAR/1/train/subject_train.txt", quote="\"", comment.char="")
> 
>   View(subject_train)
>   
> X_train <- read.table("C:/Users/CA/Downloads/HAR/1/train/X_train.txt", quote="\"", comment.char="")
> 
>   View(X_train)
>   
> y_train <- read.table("C:/Users/CA/Downloads/HAR/1/train/y_train.txt", quote="\"", comment.char="")
> 
>   View(y_train)
>   
> features <- read.table("C:/Users/CA/Downloads/HAR/1/features.txt", quote="\"", comment.char="")
> 
> activity_labels <- read.table("C:/Users/CA/Downloads/HAR/1/activity_labels.txt", quote="\"", comment.char="")
> 
>   View(activity_labels)
>   

#1. Next, I merged the training and the test sets to create one data set.

> Subject <- rbind(subject_train, subject_test)
> 
> X <- rbind(X_train, X_test)
> 
> Y <- rbind(y_train, y_test)
> 
> Data <- cbind(Subject, X, Y)
> 

#2. Extracted the mean and sd for each measurement (Extracted only the measurements on the mean and standard deviation for each measurement.) 

> XMean <- colMeans(X, na.rm = TRUE)
> 
> X_SD <- X %>% summarise_if(is.numeric, sd)
> 
> X <- rbind(XMean, X_SD)
> 

> YMean <- colMeans(Y, na.rm = TRUE)
> 
> Y_SD <- Y %>% summarise_if(is.numeric, sd)
> 
> Y <- rbind(YMean, Y_SD)
> 

> Data2 <- cbind(Subject, X_SD, Y_SD)
> 


#3. Used Data2 the descriptive activity names in the features file to name the activities in the data set preserving anonymity by not including references to Subjects.


> Data3 <- cbind(features, X_SD, Y_SD)
> 

#4. Labeled Data3 with descriptive variable names – I choose Standard Deviation or “SD” and to keep the features nomenclature as it related to the original datasets so researchers could find the information in the raw data, as necessary. I used this website: https://www.statology.org/how-to-rename-data-frame-columns-in-r/


> names(Data3)[3-50] <- "SD"
> 
> names(Data3)[1] <- "Incident"
> 
> names(Data3)[2] <- "Features"
> 
> names(Data3)[47] <- "SD"
> 

5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject. I decided to not identify subjects, to preserve anonymity and to focus on the necessary data: SD, which is “Standard Deviation” for each activity. Therefore, it is my argument that a tidy dataset does not contain Subject information. I then saved my last dataset (Data6) as a text after installing writeexl and using the write.xlsx function. Since I have a PC, I can use my Excel to save the data as a text and an .xls file I can manipulate later using Excel, if I choose.


> Data4 <- cbind(activity_labels, X_SD, Y_SD)
> 
> Data5 <- colMeans(Data4[sapply(Data4, is.numeric)]) 
> 
> View(Data5)
> 
> Data5 <- Data4[, c("SD")]  
> 
> Data6 <- cbind(activity_labels, Data5)
> 
> View(Data6) 
> 
> names(Data6)[1] <- "Activity_No."
> 
> names(Data6)[2] <- "Activity"
> 
> names(Data6)[3] <- "SD"
> 
> installed.packages(writexl)
> 
> write_xlsx(Data6,"C:\\Users\\CA\\Documents\\Data6.xlsx")
> 
