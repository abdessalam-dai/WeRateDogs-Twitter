# WeRateDogs Twitter Data Wrangling and Analysis
## by Abdessalam Dai


## Overview

> This is the second project in Udacity's Nanodegree Program for Data Analysis. In this project, I wrangled WeRateDogs Twitter data to create interesting and trustworthy analyses and visualizations. The Twitter archive is great, but it only contains very basic tweet information. Additional gathering, then assessing and cleaning was required for "Wow!"-worthy analyses and visualizations. I documented my wrangling efforts in a Jupyter Notebook, plus showcase them through analyses and visualizations using Python (and its libraries). (Finalized on 20 December 2022).

## Data Gathering

#### The WeRateDogs Twitter archive
We have downloaded this file manually: `twitter_archive_enhanced.csv`. Once it was downloaded, we uploaded it and read the data into a pandas DataFrame.

#### The tweet image predictions
This file (image_predictions.tsv) is present in each tweet according to a neural network. It is hosted on Udacity's servers and was downloaded programmatically using the Requests library and the following URL: https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv

#### Additional data from the Twitter API
We gathered each tweet's retweet count and favorite ("like") count. Using the tweet IDs in the WeRateDogs Twitter archive, we queried the Twitter API for each tweet's JSON data using Python's Tweepy library and stored each tweet's entire set of JSON data in a file called tweet_json.txt file.

Each tweet's JSON data should be written to its own line. Then we read this .txt file line by line into a pandas DataFrame with tweet ID, retweet count, and favorite count.


## Assessing Data

Using both visual assessment and programmatic assessments, we were able to identify the following issues:

#### Quality Issues
- Unwanted records that represent retweets replies.
- Non common dog names in the name column, such as 'a', 'o', 'actually', 'all', 'an', 'by', 'getting', 'his', 'incredibly', 'infuriating', 'just', 'life', 'light', 'mad', 'my', 'not', 'officially', 'old', 'one', 'quite', 'space', 'such', 'the', 'this', 'unacceptable', 'very'.
- Wrong datatype of tweet_id, which is int64.
- Wrong datatype of timestamp, which is object.
- Some records have missing values in the expanded_urls column.
- The types of dogs in columns p1, p2, and p3 don't have the same format, some of them are lowercase, others are titlecase.
- Wrong datatype of tweet_id, which is int64.
- There are 2075 records in the image predictions dataset, meaning that we have 281 missing records, because there are 2356 records in the Data Archive dataset.
- Wrong datatype of id_str, which is int64.
- There are 2325 records present in the additional JSON dataset. meaning that we have 31 missing records.

#### Tidiness Issues
- The columns doggo, floofer, pupper and puppo are unnecessary. The names of dogs should be stored in one column which is name.
- Unnecessary columns : retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp, in_reply_to_status_id, in_reply_to_user_id, rating_denominator, and source.
- Instead of keeping the three types that are in p1, p2, and p3, we only need the one with the heighest probability.
- No need for records in which the image is predicted as a non dog (ie. p1_dog, p2_dog and p3_dog are all False).
- No need for the img_num column.
- The column name of id_str should be changed to tweet_id so that we can merege the three datasets.


## Cleaning Data

After assessing the data, we cleaned the data by defining, coding, and testing. We defined the cleaning process by writing down the definition of the cleaning tasks that needed to be performed. Then we coded the cleaning tasks by writing functions to programmatically perform those cleaning tasks. Finally, we tested our cleaning code by running it and making sure the cleaning tasks were performed correctly.

We used the following techniques to address the problems we mentioned in the previous section after making copies of the three datasets:

>- Removed unnecessary columns.
- Dropped data points for retweets or replies.
- Records with unusual dog names were deleted.
- Using the df.apply and pd.to datetime methods, the datatypes of the columns were changed to what they should be.
- Records that lacked values in the expanded urls column were deleted.
- All dog breeds have been changed to lowercase.
- Added dog names to the name column and removed the doggo, floofer, pupper, and puppo columns.
- Only the most assured dog breed level was chosen.
- Dropped records that the neural network predictions consider to be non-dogs.
- The three datasets were eventually combined into one dataset, df master, and saved.