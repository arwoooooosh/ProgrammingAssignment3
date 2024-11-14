# Code Book

The `run_analysis.R` script performs data preparation followed by the 5 steps required as described in the course project's definition.

## 1. Download the Dataset

-   Dataset downloaded and extracted under the folder called `UCI HAR Dataset`.

## 2. Assign Each Data to Variables

-   `features` \<- `features.txt`: 561 rows, 2 columns\
    The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals `tAcc-XYZ` and `tGyro-XYZ`.

-   `activities` \<- `activity_labels.txt`: 6 rows, 2 columns\
    List of activities performed when the corresponding measurements were taken and its codes (labels).

-   `subject_test` \<- `test/subject_test.txt`: 2947 rows, 1 column\
    Contains test data of 9/30 volunteer test subjects being observed.

-   `x_test` \<- `test/X_test.txt`: 2947 rows, 561 columns\
    Contains recorded features test data.

-   `y_test` \<- `test/y_test.txt`: 2947 rows, 1 column\
    Contains test data of activities' code labels.

-   `subject_train` \<- `test/subject_train.txt`: 7352 rows, 1 column\
    Contains train data of 21/30 volunteer subjects being observed.

-   `x_train` \<- `test/X_train.txt`: 7352 rows, 561 columns\
    Contains recorded features train data.

-   `y_train` \<- `test/y_train.txt`: 7352 rows, 1 column\
    Contains train data of activities' code labels.

## 3. Merges the Training and the Test Sets to Create One Data Set

-   `X` (10299 rows, 561 columns) is created by merging `x_train` and `x_test` using `rbind()` function.
-   `Y` (10299 rows, 1 column) is created by merging `y_train` and `y_test` using `rbind()` function.
-   `Subject` (10299 rows, 1 column) is created by merging `subject_train` and `subject_test` using `rbind()` function.
-   `Merged_Data` (10299 rows, 563 columns) is created by merging `Subject`, `Y`, and `X` using `cbind()` function.

## 4. Extracts Only the Measurements on the Mean and Standard Deviation for Each Measurement

-   `TidyData` (10299 rows, 88 columns) is created by subsetting `Merged_Data`, selecting only columns: `subject`, `code`, and the measurements on the mean and standard deviation (`std`) for each measurement.

## 5. Uses Descriptive Activity Names to Name the Activities in the Data Set

-   Entire numbers in `code` column of the `TidyData` replaced with corresponding activity taken from the second column of the `activities` variable.

## 6. Appropriately Labels the Data Set with Descriptive Variable Names

-   `code` column in `TidyData` renamed into `activities`.
-   All `Acc` in column names replaced by `Accelerometer`.
-   All `Gyro` in column names replaced by `Gyroscope`.
-   All `BodyBody` in column names replaced by `Body`.
-   All `Mag` in column names replaced by `Magnitude`.
-   All start with character `f` in column names replaced by `Frequency`.
-   All start with character `t` in column names replaced by `Time`.

## 7. From the Data Set in Step 4, Creates a Second, Independent Tidy Data Set with the Average of Each Variable for Each Activity and Each Subject

-   `FinalData` (180 rows, 88 columns) is created by summarizing `TidyData`, taking the means of each variable for each activity and each subject, grouped by subject and activity.
-   Export `FinalData` into `FinalData.txt` file.
