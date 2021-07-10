# 3Class4
#After reading about the project at http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones , I downloaded the datasets at  https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip, saved them locally in a chosen working directory, then unzipped, them, read the ReadMe and Features files, then mapped the datasets manually on a piece of paper to help me keep track.  
#In R, I loaded packages via the lower left pane Packages tab

# I downloaded and unzipped the datasets, therefore being able to map it by hand. I downloaded from this website:   https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip
# I loaded the Test and Train datasets  by importing each separately using the import text function in the upper right pane. I did the same for the source variable names for the Test and Training data sets, and I loaded the activity labels. 	

# I began to create one R script called run_analysis.R with the first of five tasks:  using the rbind() function to merge the 18 training and test datasets to create one data set of each. I followed a tutorial at this web address:   https://www.datacamp.com/community/tutorials/merging-datasets-r . I combined the Test and Training data frames using rbind.

# My next tasks were: extract the (a) mean and (b) standard deviation for each measurement. Regarding how to obtain the standard deviation of multiple columns in a dataframe using dplyr functions, I used instructions from this website: https://www.datasciencemadesimple.com/get-standard-deviation-of-a-column-in-r-2/ .

# I then used descriptive activity names to name the activities in the data set. I also pared down the data frames to include mean and standard deviation variables. 

# I also appropriately labeled the data set with descriptive variable names, and combined the Test and Training data frames into one dataframe (Data) with the measurements and activities
