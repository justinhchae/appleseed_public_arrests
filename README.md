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







