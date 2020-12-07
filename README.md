readme

# appleseed_public_arrests data

Project Title: Exploring Detailed Chicago Police Arrest Data

## Project Summary 
This [data](https://github.com/justinhchae/appleseed_public_arrests/tree/main/data) is based on a preimilary analysis of detailed arrest data from the [Chicago Data Portal](https://data.cityofchicago.org/). The data is significant becuase the data, at times, has not been avaialble at all, or it was available without certain datapoints. For instance, these arrest records contain the datetime stamps for arrest, lockup, release from lockup and bond date which have not always been available.


Fortunately, we were able to obtain access to the full dataset thanks to the Data Portal team. Based on a bulk download of CPD data, we transformed several columns to help make sense of the data. For example, we extracted year, month, and time of day into separate fields. In addition, we classified every charge into a set of grouped categories. In the resulting dataset, we believe we've added value to this publically available data by categorizing date and time columns and adding classifications to charge descriptions. 


![alt text](https://github.com/justinhchae/appleseed_public_arrests/blob/main/figures/Arrests_Distribution_1_Ramp.png?raw=true)


## This Data
To provide transparency in our analysis and to assist others who many be interested in this data, we are sharing a redacted version of the arrest data.

To protect the privacy of individuals, this redacted version of the primary data set removes information such as name, cb number, and date.
However, the resulting fields in the redacted table represent nearly all the data used in the analysis and may be quite helpful in other areas.

This data is a single table avaialble in either a zipped csv file or a pickle file (exported from the Python Pandas Library)


![alt text](https://github.com/justinhchae/appleseed_public_arrests/blob/main/figures/Arrests_Distribution_3_Histogram.png?raw=true)

### The fields in this data about the person include:

| race  |

* Race is a string represented as a categorical data type.
* Example: BLACK, WHITE HISPANIC, ASIAN / PACIFIC ISLANDER


![alt text](https://github.com/justinhchae/appleseed_public_arrests/blob/main/figures/Arrests_Charges_3_race.png?raw=true)

### The fields in this data about the event include:

| district | beat  |

* Police District and Police Beat number are numbers represented as a categorical data types.
* Example: District (6, 11, 7). Beat (623, 414, 1122).

![alt text](https://github.com/justinhchae/appleseed_public_arrests/blob/main/figures/Arrests_Charges_4_district.png?raw=true)

### The fields in this data about the charges include:

| charge_1_statute | charge_1_description  | charge_1_type | charge_1_class  |

* Charge Statute, Descriptions, Type, and Class are provided exactly as given by the Chicago Data Portal and are represented as text.
* Example: Statute (720 ILCS 5.0/12-1-A). Description (DRIVING/NEVER ISSUED LICENSE). Type (M for Misdemeanor and F for Felony). Class (1 for Class 1 through Class 4, A, B, X...)

![alt text](https://github.com/justinhchae/appleseed_public_arrests/blob/main/figures/Arrests_Charges_2_detailed.png?raw=true)

### The derived fields in this data about the charges include:

| charge_1_cat  | charge_1_cat_macro  | police_related_1  | forcible_1  |

* Charge Category and Charge Category Macro are a two-tiered classification system that encode the charge descriptions represented as categorical data types.
* Example: charge_1_description (CANNABIS - POSSESS LESS THAN 2.5 GRMS) becomes charge_1_cat (CANNABIS) and charge_1_cat_macro (Drug)

* Police Related and Foricible encode additional dimentions about the charge represented as categorical data types (boolean).
* Example: charge_1_description (RESISTING/OBSTRUCT/PC OFF/CORR EMP/FRFTR INJ) becomes police_related_1 (TRUE) and charge_1_description (AGG BATTERY/PEACE OFFICER) becomes police_related_1 (TRUE) and forcible_1 (TRUE).

### The derived date and time fields in this data include:

| arrest_year  | arrest_month  | arrest_time  | lockup_time  | release_time  |

* Each date or time field is extracted from a datetime data type and represented here as integers (year and month) and 24-hour time values (objects).
* Example: arrest_year (2018, 2019, 2020, ...). arrest_month (1, 2, 3, ...). arrest_time (17:00:00, 18:11:00, 20:16:00, ...)
* Note: Time timestamp values are created using the [Pandas dt.time extractor](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html) based on the original data's datetime columns.

![alt text](https://github.com/justinhchae/appleseed_public_arrests/blob/main/figures/Arrests_Charges_6_time.png?raw=true)


## How to Use this Data
* The easiest method is to download and unzip the csv file and analyze the data with any system of your choosing. However, for convenience we exported a pickled file from a Pandas DataFrame. The pickled file has the data types encoded directly into the file so categorical values maintain their categories. For instance, we leveraged Pandas DataFrames and set columns with the categorical value as a dtype.

* Download the (.pickle file)[https://github.com/justinhchae/appleseed_public_arrests/blob/main/data/arrests_analysis_public.pickle?raw=true]. From a Python 3.x environment the following code snippet may help read and process the data. 
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

# From the Author

The issue of incommunicado detention in Chicago is at least 30-years old. Although society still struggles with policing and access to justice issues, today, we have the opportunity to analyze data in a way that was previously not available. Electronic records for arrest data go as far back as 2014 and are currently updated regularly by the Chicago Data Portal. After gaining access to detailed records, we jumped at the opportunity to explore the dataset, start analyzing, and share our preliminary results with the public.

At this time, this analysis is inconclusive, but we leave you with four points:

* The data herein represents a tremendous opportunity for analysis but is still incomplete. 
* There are data quality issues that require further investigation and scrutiny — further peer review of our analysis is both necessary and welcome.
* At this stage of analysis, it is still not clear what factors are responsible for very long holding times — questions along this topic may inform next steps in research.
* Finally, as we continue to research this dataset and explore relationships to court reform, we are interested in your comments and collaboration.

## Methodology

### Source
The Data Team at Chicago Data Portal (https://data.cityofchicago.org/) granted access to detailed arrest data API for analysts at Chicago Appleseed Center for Fair Courts. Importantly this data contains the date/time stamp of arrest, lockup, release from lockup, and bond court appearance. This analysis would not be possible otherwise.


### Data
The dataset was initially bulk downloaded on 14 October 2020 and contains 535,314 records. After initial analysis of the data and in preparation for this post, the dataset was downloaded again on 27 October 2020 and contains a total of 536,770 records. In both cases, a cleaning routine was applied in two phases. First, records with erroneous dates were filtered out, i.e. those that produce negative holding times. Second, the lead charge description was standardized from several thousand variations into two tiers of categories. In sum, the analysis accounts for approximately 536,000 records spanning a period of 6 years from 2014 to 2020.


### Erroneous Records
To calculate time phases in arrest data, this analysis assumes there is a timeline of linear events that starts with arrest, proceeds to lockup, and ends in either a release from lockup or a court date. For example, erroneous records are tagged and omitted wherever the lockup or release date pre-dates the arrest date. There are other records that may be considered erroneous such as when the age of a person is over 100 years old (these exist); however, since the age of a person is not taken into account, as long as the other fields are valid, they are not omitted. Least, but perhaps most importantly, there are a number of extreme outliers in holding times that were excluded for this analysis. For example, there is a single holding time at 1,900 hours and a dozen or so between 100 and 500 hours - are these real cases or clerical errors?


### Charge Categorization
To make sense of charges, this analysis categorizes each record according to two tiers. Our senior staff attorney hand classified several thousand records to create a mapping key from charge description to charge category to create 39 detailed classifications (Tier 2). The detailed classifications were further grouped into eight primary categories (Tier 1). Using the mapping table and classification guide, we leveraged a combination of algorithms to match and classify each arrest record’s charges to a category.

### Charge Classification Categories

| Tier 2 (Micro Cat) | Tier 1 (Macro Cat) |
| ------------- | ------------- |
| Violation of Release, Warrant/FTA  | CourtRelated  |
| Cannabis, Narcotics  | Drug  |
| Assault, Battery, Domestic Violence, Murder-1st Degree, Harassment/Stalking/Intimidation, Child/Minor Related, Homicide (Not 1st Degree), Kidnapping, Sex Crime, VOOP  | Person  |
| DUI, DSL, Vehicle/Traffic  | Vehicle  |
| Firearm Discharge, Weapon - Non-Firearm, Gun Possession  | Weapon  |
| Trespass, PSMV/CTTV, Criminal Damage, Arson, Retail Theft, Burglary, Theft, Robbery, Fraud/ID Theft, Fraud/Theft  | Property  |
| Tobacco, Nuisance, Disorderly/Reckless Conduct, Gambling, Resisting Arrest/Obstructing Officer, Prostitution, Registry, Escape  | PublicOrder  |
| Other  | Other  |


Although not explicitly leveraged in this story, we also applied a similar method to tagging whether a given charge is policed-related or not. In addition, whether a charge is considered a ‘forcible’ crime. For instance, a police-related charge is largely characterized by resisting arrest or assault against a police officer. Similarly, a forcible classification usually includes charges involving battery but not weapons charges. The following table is an example table used to classify the main dataset. Note: the police and forcible flags were primarily created based on the text of the charge description and not the Tier 2 classification. 

### Police Related and Forcible Flags


| Tier 2 (Micro Cat) | police_related| forcible |
| ------------- | ------------- | ------------- |
| Battery  | TRUE  | TRUE  |
| Assault  | TRUE  | FALSE  |
| Disorderly/Reckless Conduct  | TRUE  | FALSE  |
| Escape  | TRUE  | FALSE  |
| Firearm Discharge  | TRUE  | FALSE  |
| Other  | TRUE  | FALSE  |
| Resisting Arrest/Obstructing Officer  | TRUE  | FALSE  |
| Vehicle/Traffic  | TRUE  | FALSE  |

### Data Classification and Machine Learning

Classifying each arrest charge according to the aforementioned schemes proved to be a difficult task. For instance, in this analysis, it sufficed to know whether a charge was primarily concerned with Cannabis at a detailed level and then at a higher level, to know it was generally a Drug related charge. However, in just one instance out of thousands, the charge description varied wildly for a subset of cannabis charges. Further, since a given arrest may have multiple charges and the dataset is updated on a daily basis, it became clear that it is not possible to actively map each charge by hand. Worse yet, there was not a one-to-one mapping that would allow us to derive the classifications according to our chosen scheme based on the remaining fields. 

```
A Sample of Charge Descriptions
CANNABIS - MFG/DEL - 10-30 GRMS
CANNABIS - MFG/DEL - 2.5-10 GRMS
CANNABIS - MFG/DEL - 2000-5000 GRMS
CANNABIS - MFG/DEL - 30-500 GRMS
CANNABIS - MFG/DEL - 500-2000 GRMS
CANNABIS - MFG/DEL - 5000+GRMS
CANNABIS - MFG/DEL - LESS 2.5 GRMS - UNDER 18
CANNABIS - MFG/DEL - LESS THAN 2.5 GRMS
```

To solve the classification problem, we applied a matching routine in three phases. 
First, we used a dictionary to map any charges that happen to match our key directly to a class. For instance, our staff attorney provided a classification by hand for a single instance of “CANNABIS - MFG/DEL 30-500 GRMS.” This first phase accounted for about 85% of all charge classifications. 


Second, we applied a fuzzy matching algorithm (https://pypi.org/project/fuzzy-pandas/) to handle cases where the key was off by a small amount. For instance, a fuzzy match allowed the key to map a classification if the text was “GRAMS” instead of “GRMS.” This was especially useful in cases where the text of the allegation was off by just a few characters or spaces but described the same charge. This second phase accounted for between 5-10% of all charge classifications.


Third and lastly, we ran the text of the charge description through a natural language processing pipeline, trained a machine learning model on the key, and used the model to classify any remaining charges that the prior two steps missed. For instance, when the words ‘cannabis’ and ‘grms’ appear together with ‘mfg’ and ‘del’, we trained a Complement Naive Bayes algorithm (https://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.ComplementNB.html#sklearn.naive_bayes.ComplementNB) to recognise that this is most likely a Cannabis charge. This third phase accounted for between 5-10% of all charge classifications and in testing, had an accuracy of about 80%.

### Assumptions

There are three notable assumptions made in this analysis. First, the time difference between arrests and lockup, lockup and release, and arrests to release provides an accurate measure of time phases in police custody. As a result, the primary findings in this post are based on three calculated fields of arrest_to_lockup, lockup_to_release, and arrest_to_release. Second, each row represents an individual person while each column represents data about the person and their time in police custody. Third, the arrest date is the first recorded time in police custody (i.e. handcuffed and in a patrol car), the lockup date is the time a person is booked at a station house (i.e. in a jail cell), and lastly, the release date is the time when a person leaves custody (i.e. released from jail, free to go, or under other court orders).


### Data Quality
The quality of this data is open for interpretation at this time. In addition to the erroneous date issues, there are several others that may require further investigation. For instance, in the police district column, there is a single entry listed as district ‘31’ (which does not exist). Further, although we confidently leveraged a classification system with machine learning, it is the first attempt of its kind for our team. As a result it is possible, perhaps even likely, there is a small error rate in classifications.


### Privacy
To protect privacy of individuals, names, and CB numbers are removed from the dataset. However, demographic information such as race are necessarily included to profile arrest data in sufficient detail. Further, after computing the time phases from arrest to release, the original dates of lockup, release, and bond court appearance are removed from the accompanying dataset. The only remaining dates are the year and month of the arrest as well as the time of day of arrest, lockup, and release from lockup. Although it may be possible to disambiguate any dataset in this day and age, the omitted columns remove as much identifiable information as possible.


### Directions for Next Research
First, several hundred records are omitted from this analysis because they return erroneous times in detention, i.e. when the lockup date is earlier than the arrest date, it appears a person was detained for a negative amount of time. However, it is not immediately clear whether dates are erroneous due to data entry or whether the timeline of events from arrest to lockup and release is not always linear. In terms of omitted records, future analysis may benefit from scrutinizing the omitted records to (1) validate whether they should be removed and if not, (2) impute dates for erroneous records and increase the quality of this analysis. 


Second, to the best of our knowledge, our attempt to classify charge records with the two tier scheme, machine learning, and flags for police related and forcible categories is the first of its kind on this dataset. As a result, a follow-on research effort may benefit from evaluating the efficacy of this model to both classify charges and understand their meaning when combined in analysis. Applications to databases of charge descriptions from other jurisdictions may also provide interesting insights in the context of national classification systems.


Third, this initial article explores only a narrow portion of the data; however, other important features are not analyzed in detail. For instance, there are features for Felony and Misdemeanor, Charge Class, Police-Related, and Forcible that we tagged or processed but did not analyze. Further, there may be opportunities to combine arrest records with police attendance data to understand the relationships between aspects of police misconduct and excessive holding times, for example. 

