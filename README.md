# 3Class4
#After reading about the project at http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones , I downloaded the datasets at  https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip, saved them locally in a chosen working directory, then unzipped, them, read the ReadMe and Features files, then mapped the datasets manually on a piece of paper to help me keep track.  
#In R, I loaded packages via the lower left pane Packages tab

# I downloaded and unzipped the datasets, therefore being able to map it by hand. I downloaded from this website:   https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip
# I loaded the Test and Train datasets  by importing each separately using the import text function in the upper right pane. I did the same for the source variable names for the Test and Training data sets, and I loaded the activity labels. 	

# I began to create one R script called run_analysis.R with the first of five tasks:  using the rbind() function to merge the 18 training and test datasets to create one data set of each. I followed a tutorial at this web address:   https://www.datacamp.com/community/tutorials/merging-datasets-r . I combined the Test and Training data frames using rbind.

# My next tasks were: extract the (a) mean and (b) standard deviation for each measurement. Regarding how to obtain the standard deviation of multiple columns in a dataframe using dplyr functions, I used instructions from this website: https://www.datasciencemadesimple.com/get-standard-deviation-of-a-column-in-r-2/ .

# I then used descriptive activity names to name the activities in the data set. I also pared down the data frames to include mean and standard deviation variables. 

# I also appropriately labeled the data set with descriptive variable names, and combined the Test and Training data frames into one dataframe (Data) with the measurements and activities

#I downloaded the writexl package and saved my df as an excel file, in addition to text


> library(tidyr)
> library(dplyr)
> library(data.table)
> body_acc_x_test <- read.table("~/UCI HAR Dataset/test/Inertial Signals/body_acc_x_test.txt", quote="\"", comment.char="")
>   View(body_acc_x_test)
> body_acc_y_train <- read.table("~/UCI HAR Dataset/train/Inertial Signals/body_acc_y_train.txt", quote="\"", comment.char="")
>   View(body_acc_y_train)
> body_acc_z_train <- read.table("~/UCI HAR Dataset/train/Inertial Signals/body_acc_z_train.txt", quote="\"", comment.char="")
>   View(body_acc_z_train)
> body_gyro_x_train <- read.table("~/UCI HAR Dataset/train/Inertial Signals/body_gyro_x_train.txt", quote="\"", comment.char="")
>   View(body_gyro_x_train)
> body_gyro_y_train <- read.table("~/UCI HAR Dataset/train/Inertial Signals/body_gyro_y_train.txt", quote="\"", comment.char="")
>   View(body_gyro_y_train)
> body_gyro_z_train <- read.table("~/UCI HAR Dataset/train/Inertial Signals/body_gyro_z_train.txt", quote="\"", comment.char="")
>   View(body_gyro_z_train)
> total_acc_x_train <- read.table("~/UCI HAR Dataset/train/Inertial Signals/total_acc_x_train.txt", quote="\"", comment.char="")
>   View(total_acc_x_train)
> total_acc_y_train <- read.table("~/UCI HAR Dataset/train/Inertial Signals/total_acc_y_train.txt", quote="\"", comment.char="")
>   View(total_acc_y_train)
> total_acc_z_train <- read.table("~/UCI HAR Dataset/train/Inertial Signals/total_acc_z_train.txt", quote="\"", comment.char="")
>   View(total_acc_z_train)
> body_acc_x_train <- read.table("~/UCI HAR Dataset/train/Inertial Signals/body_acc_x_train.txt", quote="\"", comment.char="")
>   View(body_acc_x_train)
> subject_train <- read.table("~/UCI HAR Dataset/train/subject_train.txt", quote="\"", comment.char="")
>   View(subject_train)
> X_train <- read.table("~/UCI HAR Dataset/train/X_train.txt", quote="\"", comment.char="")
>   View(X_train)
> y_train <- read.table("~/UCI HAR Dataset/train/y_train.txt", quote="\"", comment.char="")
>   View(y_train)
> body_acc_x_test <- read.table("~/UCI HAR Dataset/test/Inertial Signals/body_acc_x_test.txt", quote="\"", comment.char="")
>   View(body_acc_x_test)
> body_acc_y_test <- read.table("~/UCI HAR Dataset/test/Inertial Signals/body_acc_y_test.txt", quote="\"", comment.char="")
>   View(body_acc_y_test)
> body_acc_z_test <- read.table("~/UCI HAR Dataset/test/Inertial Signals/body_acc_z_test.txt", quote="\"", comment.char="")
>   View(body_acc_z_test)
> body_gyro_x_test <- read.table("~/UCI HAR Dataset/test/Inertial Signals/body_gyro_x_test.txt", quote="\"", comment.char="")
>   View(body_gyro_x_test)
> body_gyro_y_test <- read.table("~/UCI HAR Dataset/test/Inertial Signals/body_gyro_y_test.txt", quote="\"", comment.char="")
>   View(body_gyro_y_test)
> body_gyro_z_test <- read.table("~/UCI HAR Dataset/test/Inertial Signals/body_gyro_z_test.txt", quote="\"", comment.char="")
>   View(body_gyro_z_test)
> body_gyro_z_test <- read.table("~/UCI HAR Dataset/test/Inertial Signals/body_gyro_z_test.txt", quote="\"", comment.char="")
>   View(body_gyro_z_test)
> total_acc_x_test <- read.table("~/UCI HAR Dataset/test/Inertial Signals/total_acc_x_test.txt", quote="\"", comment.char="")
>   View(total_acc_x_test)
> total_acc_y_test <- read.table("~/UCI HAR Dataset/test/Inertial Signals/total_acc_y_test.txt", quote="\"", comment.char="")
>   View(total_acc_y_test)
> total_acc_z_test <- read.table("~/UCI HAR Dataset/test/Inertial Signals/total_acc_z_test.txt", quote="\"", comment.char="")
>   View(total_acc_z_test)
> subject_test <- read.table("~/UCI HAR Dataset/test/subject_test.txt", quote="\"", comment.char="")
>   View(subject_test)
> X_test <- read.table("~/UCI HAR Dataset/test/X_test.txt", quote="\"", comment.char="")
>   View(X_test)
> y_test <- read.table("~/UCI HAR Dataset/test/y_test.txt", quote="\"", comment.char="")
>   View(y_test)
> activity_labels <- read.table("~/UCI HAR Dataset/activity_labels.txt", quote="\"", comment.char="")
>   View(activity_labels)
> features <- read.table("~/UCI HAR Dataset/features.txt", quote="\"", comment.char="")
>   View(features)
> AccelX <- rbind(body_acc_x_train, body_acc_x_test)
> AccelY <- rbind(body_acc_y_train, body_acc_y_test)
> AccelZ <-rbind(body_acc_z_train, body_acc_z_test)

> GyroX <- rbind(body_gyro_x_train, body_gyro_x_test)
> GyroY <- rbind(body_gyro_y_train, body_gyro_y_test)
> GyroZ <- rbind(body_gyro_z_train, body_gyro_z_test)

> TotalAccX <- rbind(total_acc_x_train, total_acc_x_test)
> TotalAccY <- rbind(total_acc_y_train, total_acc_y_test)
> TotalAccZ <- rbind(total_acc_z_train, total_acc_z_test)

> Subject <- rbind(subject_train, subject_test)
> X <- rbind(X_train, X_test)
> Y <- rbind(y_train, y_test)
> AccelXMean <- colMeans(AccelX, na.rm = TRUE)
> AccelX_SD <- AccelX %>% summarise_if(is.numeric, sd)

> AccelYMean <- colMeans(AccelY, na.rm = TRUE)
> AccelY_SD <- AccelY %>% summarise_if(is.numeric, sd)

> AccelZMean <- colMeans(AccelZ, na.rm = TRUE)
> AccelZ_SD <- AccelZ %>% summarise_if(is.numeric, sd)

> GyroXMean <- colMeans(GyroX, na.rm = TRUE)
> GyroX_SD <- GyroX %>% summarise_if(is.numeric, sd)

> GyroYMean <- colMeans(GyroY, na.rm = TRUE)
> GyroY_SD <- GyroY %>% summarise_if(is.numeric, sd)

> GyroZMean <- colMeans(GyroZ, na.rm = TRUE)
> GyroZ_SD <- GyroZ %>% summarise_if(is.numeric, sd)

> TotalAccXMean <- colMeans(TotalAccX, na.rm = TRUE)
> TotalAccX_SD <- TotalAccX %>% summarise_if(is.numeric, sd)

> TotalAccYMean <- colMeans(TotalAccY, na.rm = TRUE)
> TotalAccY_SD <- TotalAccY %>% summarise_if(is.numeric, sd)

> TotalAccZMean <- colMeans(TotalAccZ, na.rm = TRUE)
> TotalAccZ_SD <- TotalAccZ %>% summarise_if(is.numeric, sd)

> SubjectMean <- colMeans(Subject, na.rm = TRUE)
> Subject_SD <- Subject %>% summarise_if(is.numeric, sd)

> XMean <- colMeans(X, na.rm = TRUE)
> X_SD <- X %>% summarise_if(is.numeric, sd)

> YMean <- colMeans(Y, na.rm = TRUE)
> Y_SD <- Y %>% summarise_if(is.numeric, sd)
> AccelX_Mean_SD <- rbind(AccelXMean, AccelX_SD)
> AccelY_Mean_SD <- rbind(AccelYMean, AccelY_SD)
> AccelZ_Mean_SD <- rbind(AccelZMean, AccelZ_SD)
> GyroX_Mean_SD <- rbind(GyroXMean, GyroX_SD) 
> GyroY_Mean_SD <- rbind(GyroYMean, GyroY_SD)
> GyroZ_Mean_SD <- rbind(GyroZMean, GyroZ_SD)
> TotalAccX_Mean_SD <- rbind(TotalAccXMean, TotalAccX_SD)
> TotalAccY_Mean_SD <- rbind(TotalAccYMean, TotalAccY_SD) 
> TotalACCZ_Mean_SD <- rbind(TotalAccZMean, TotalAccZ_SD)
> X_Mean_SD <- rbind(XMean, X_SD)
> Y_Mean_SD <- rbind(YMean, Y_SD)
> Subject <- rbind(SubjectMean, Subject_SD)
> Data <- rbind(AccelX_Mean_SD, AccelY_Mean_SD, AccelZ_Mean_SD, GyroX_Mean_SD, GyroY_Mean_SD,  GyroZ_Mean_SD, TotalAccX_Mean_SD, TotalAccY_Mean_SD, TotalACCZ_Mean_SD)
package ‘writexl’ successfully unpacked and MD5 sums checked

The downloaded binary packages are in
	C:\Users\CA\AppData\Local\Temp\RtmpmizxZQ\downloaded_packages
> installed.packages(writexl)
> install.packages("writexl")
> library(writexl)
> write_xlsx(Data,"C:\\Users\\CA\\Documents\\DATA.xlsx")
