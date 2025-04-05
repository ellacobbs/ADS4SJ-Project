# CAHOOTS
The purpose of this script is to be used to clean up and analyze CAD data from Eugene, Oregon in order to better analyze the impact that the 
organization CAHOOTS has had on the community.

 # Packages
 The scripts each use a variety of packages and as a result start by importing pandas, numpy, LinearRegression from sklearn,norm from scipy, warnings, and matplotlib.pyplot. These packages are needed in order to manipulate the dataframes, perform mathematical equations, linear regression analysis and create visualizations.

 To ensure that the code will run, these packages need to be installed:
 - pandas from PyPi
 - Numpy already comes with Python
 - scipy
 - from scipy, can install scikit-learn
 - matplotlib

 # Cleaning
 The first step in the file is to run a filter using warnings to hide any warnings that may appear. 
 The cleaning portion of the file begins by first importing the CAD csv and assigning it to simply `cad`. Then, uses .head() in order to view the data to ensure 
 it was correctly imported. Next, unnessecary columns for the project are dropped only leaving information about the call's zipcode, the primary and responding unit call signs, 
 as well as the date and time of call to start the creation of the clean dataframe, cad_clean. NA values are dropped during this step as well. The zipcode column is converted 
 from strings to integers and only calls made within zipcodes found in the Eugene zipcode array `zips` are kept. Columns in the dataframe are then renamed for clarity and more 
 accessibility. The call signs for CAHOOTS are then defined, some specifically outlined in `ch` and the more general requirements seen in `ch_r`. Using these call signs, the 
 Called and Responded column unit call signs are converted to CAHOOTS if they line up with the criteria of `ch` and `ch_r`. Then, in the date time column, the time is dropped and 
 the date is converted to datetime using pandas. The final clean dataframe is viewed once more, and saved as cad_clean through a file path placing the new data frame in a folder called "data". 


 # Analysis
 Similarly to the cleaning script, the analysis file starts by importing packages and hiding warnings.
 Next, the date column is converted to datetime using pd.to_datetime as it does not always transfer over from the cleaning script. 
 Then, the date that CAHOOTS added a second van and expanded their operating hours is defined as `service`. Using that service date, a table containing calls a year before this date is defined as `before`, and another table including the date and up to a year following the service date is called `after`. The number of calls in both of these tables are assigned
 to `before_size` and `after_size`. Then, using these before and after dataframes, two more were created for each timeframe each including a table where CAHOOTS were called and
 responded (regular CAHOOTS calls) and where they were not orignally called, but responded (diverted to CAHOOTS calls). CAHOOTS calls before the service date are saved under 
 `ch_before` and diverted calls before are saved under `ch_after`. The same thing is done for diverted calls, saved under `divert_before` and `divert_after`. Like the previous step,
 the number of calls in each of these situations were saved under `calls_before`, `divert_before_num`, `calls_after`, and `divert_after_num` in the same order they were just described.
 
 For the first step of analysis, a function defined as z_score calculates the z-score of two proportions, in this case, the proportion of the number of CAHOOTS or diverted calls
 before and after the service date, as well as the p-value of that z-score. The c1 argument is the number of calls for CAHOOTS or that CAHOOTS were diverted to in the year before,
 c2 being the same but for the year after.n1 is the total number of calls for the whole year before, and n2 is the total number of calls for the year after. The function is used 
 to calculate the z-score and p-value of the proportion of CAHOOT calls, assigned to `chcalls_z` and the same for calls diverted to CAHOOTS, `divert_z`. 

 Then for the linear regression portion, first a portion of the dataset is taken to only include calls before 2022 defined as `usable` and another is made from that table where CAHOOTS responded, saved as `ch_calls`, and where they did not which is `other_calls`. Then, seperate proportions of 
 CAHOOTS calls are calculated for every month in 2016 - 2021 using these data sets. These proportions are then put into their own dataframe corresponding
 with the year they came from, `monthly_averages`. Another table, `months_x` is made to convert the datetime values in the "Date" column to an ordinal value using to_ordinal so they can be used in the linear regression analysis. Then, the x-variable for the linear regression is defined as the ordinal date column from that dataset, and the y-variable as the 
 CAHOOTS percentage from the one before. Each month and year used in the usable data is defined simply as `months` and `years` to be used for visualizations later. The labels of each month are also gathered in `month_labels`. The months to be used for the linear regression
prediction is also created starting at the earliest date and ending at the end of 2035, about ten years from now. These values can be found under `future_months`. These months and their percentage predictions are saved in the data frame `month_predictions`. A final table `divert_props` is created to calculate the percentage of calls diverted before and after the expansion.

The final section of the analysis script is the visualizations section. This starts with a simple bar graph of the values just created in `divert_props`, showing off the percentages before and after the expansion. Then, a line of the predictions made through linear regression is graphed along with a point for the percentage of calls handled per month with the data currently available. Finally, these same percentages of calls per month are graphed as a line graph with a line at the beginning of 2017 representing when the expansion occurred.
 
