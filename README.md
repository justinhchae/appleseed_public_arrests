# appleseed_public_arrests data

Project Title: Exploring Detailed Chicago Police Arrest Data

## Project Summary 
This data is based on a preimilary analysis of detailed arrest data from the Chicago Data Portal. The data is significant becuase the data, at times, has not been avaialble at all, or it was available without certain datapoints.
For instance, these arrest records contain the datetime stamps for arrest, lockup, release from lockup and bond date. 


Based on a bulk download of this data, we transformed several columns to help make sense of the data. 
For example, we extracted year, month, and time of day into separate fields. In addition, we classified every charge into a set of grouped categories.

## This Data
To provide transparency in our analysis and to assist others who many be interested in this data, we are sharing a redacted version of the arrest data.

To protect the privacy of individuals, this redacted version of the primary data set removes information such as name, cb number, and date.
However, the resulting fields in the redacted table represent nearly all the data used in the analysis and may be quite helpful in other areas.


This data is a single table avaialble in either a zipped csv file or a pickle file (exported from the Python Pandas Library)


###### The fields in this data about the person include:

| race  |

* Race is a string represented as a categorical data type.
* Example: BLACK, WHITE HISPANIC, ASIAN / PACIFIC ISLANDER


###### The fields in this data about the event include:

| district | beat  |

* Police District and Police Beat number are numbers represented as a categorical data types.
* Example: District (6, 11, 7). Beat (623, 414, 1122).


###### The fields in this data about the charges include:

| charge_1_statute | charge_1_description  | charge_1_type | charge_1_class  |

* Charge Statute, Descriptions, Type, and Class are provided exactly as given by the Chicago Data Portal and are represented as text.
* Example: Statute (720 ILCS 5.0/12-1-A). Description (DRIVING/NEVER ISSUED LICENSE). Type (M for Misdemeanor and F for Felony). Class (1 for Class 1 through Class 4, A, B, X...)


###### The derived fields in this data about the charges include:

| charge_1_cat  | charge_1_cat_macro  | police_related_1  | forcible_1  |

* Charge Category and Charge Category Macro are a two-tiered classification system that encode the charge descriptions represented as categorical data types.
* Example: charge_1_description (CANNABIS - POSSESS LESS THAN 2.5 GRMS) becomes charge_1_cat (CANNABIS) and charge_1_cat_macro (Drug)

* Police Related and Foricible encode additional dimentions about the charge represented as categorical data types (boolean).
* Example: charge_1_description (RESISTING/OBSTRUCT/PC OFF/CORR EMP/FRFTR INJ) becomes police_related_1 (TRUE) and charge_1_description (AGG BATTERY/PEACE OFFICER) becomes police_related_1 (TRUE) and forcible_1 (TRUE).

###### The derived date and time fields in this data include:

| arrest_year  | arrest_month  | arrest_time  | lockup_time  | release_time  |


* Each date or time field is extracted from a datetime data type and represented here as integers (year and month) and 24-hour time values (objects).
* Example: arrest_year (2018, 2019, 2020, ...). arrest_month (1, 2, 3, ...). arrest_time (17:00:00, 18:11:00, 20:16:00, ...)
* Note: Time timestamp values are created using the pandas dt.time extractor based on the original data's datetime columns.


## How to Use this Data
* The easiest method is to download and unzip the csv file and analyze the data with any system of your choosing. However, for convenience we exported a pickled file from our Python project. The pickled file has the data types encoded directly into the file so categorical values maintain their categories. For instance, we leveraged Pandas DataFrames and set columns with the categorical value as a dtype.

* Download the .pickle file. From a Python 3.x environment the following code snippet may help read and process the data. 
```
# given a file (arrests_analysis_public.pickle) in a folder called data

import pandas as pd

df = pd.read_pickle('data/arrests_analysis_public.pickle')

print(df.head())

# >>> output:

    race district  beat bond_type_cd bond_amt     charge_1_statute  \...
0  BLACK        6  0623        IBOND     1500  720 ILCS 5.0/12-1-A  \...
1  BLACK        6  0634        IBOND     1500   720 ILCS 550.0/4-A  \...
```





