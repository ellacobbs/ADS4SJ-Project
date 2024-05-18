# ADS4SJ-Project
The purpose of this script is to be used to clean up and analyze CAD data from Eugene, Oregon in order to better analyze the impact that the 
organization CAHOOTS has had on the community.

 # Packages
 The script starts by importing pandas and numpy. These packages are needed in order to manipulate the dataframes and perform mathematical equations.

 # Cleaning
 The cleaning portion of the file begins by first importing the CAD csv and assigning it to simply "cad". Then, uses .head() in order to view the data to ensure 
 it was correctly imported. Next, unnessecary columns for the project are dropped only leaving information about the call's zipcode, the primary and responding unit call signs, 
 as well as the date and time of call to start the creation of the clean dataframe, cad_clean. NA values are dropped during this step as well. The zipcode column is converted 
 from strings to integers and only calls made within zipcodes found in the Eugene zipcode array "zips" are kept. Columns in the dataframe are then renamed for clarity and more 
 accessibility. The call signs for CAHOOTS are then defined, some specifically outlined in "ch" and the more general requirements seen in "ch_r". Using these call signs, the 
 Called and Responded column unit call signs are converted to CAHOOTS if they line up with the criteria of "ch" and "ch_r". Then, in the date time column, the time is dropped and 
 the date is converted to datetime using pandas. The final clean dataframe is viewed. 

 Next, the date that CAHOOTS added a second van and expanded their operating hours is defined as "service". Using that service date, a table containing calls a year before this date 
 is defined as "before", and another table including the date and up to a year following the service date is called "after". The number of calls in both of these tables are assigned
 to "before_size" and "after_size". Then, using these before and after dataframes, two more were created for each timeframe each including a table where CAHOOTS were called and
 responded (regular CAHOOTS calls) and where they were not orignally called, but responded (diverted to CAHOOTS calls). CAHOOTS calls before the service date are saved under 
 "ch_before" and diverted calls before are saved under "ch_after". The same thing is done for diverted calls, saved under "divert_before" and "divert_after". Like the previous step,
 the number of calls in each of these situations were saved under "calls_before", "divert_before_num", "calls_after", and "divert_after_num" in the same order they were just described.

 # Analysis
 For the first step of analysis, a function defined as z_score calculates the z-score of two proportions, in this case, the proportion of the number of CAHOOTS or diverted calls
 before and after the service date. The c1 argument is the number of calls for CAHOOTS or that CAHOOTS were diverted to in the year before, c2 being the same but for the year after.
 n1 is the total number of calls for the whole year before, and n2 is the total number of calls for the year after. The function is used to calculate the z-score of the proportion of
 CAHOOT calls, assigned to "chcalls_z" and the same for calls diverted to CAHOOTS, "divert_z". 
