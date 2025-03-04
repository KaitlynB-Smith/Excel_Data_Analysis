# Global Landslide Data Analysis - Excel
Understanding the drivers behind global landslide events is crucial for mitigation and prevention. This project utilizes Excel and Tableau to clean, explore, and visualize a global landslide dataset. The goal of this project is to identify patterns in landslide frequency, pinpoint factors that contribute to their destructive nature, and provide a deeper understanding of global landslide trends.

--- 

# Data Overview
## About the Dataset
This is a comprehensive landslide dataset obtained from [NASA's Open Data Portal](https://data.nasa.gov/Earth-Science/Global-Landslide-Catalog-Export/dd9e-wu2v/about_data).This data is comprised of 31 columns and 11,033 rows that includes information about the time, date, locations, news sources, triggers, sizes, settings, fatality count, injury count, and descriptions of individual landslide events. 

## Links to Dataset
- Click [here](https://data.nasa.gov/Earth-Science/Global-Landslide-Catalog-Export/dd9e-wu2v/data_preview) to preview the dataset on NASA's Open Data Portal.
- Click [here](https://catalog.data.gov/dataset/global-landslide-catalog-export) to access the data on Data.gov

## Credit to Original Authors of the Dataset
-	Kirschbaum, D. B., Adler, R., Hong, Y., Hill, S., & Lerner-Lam, A. (2010). A global landslide catalog for hazard applications: method, results, and limitations. Natural Hazards, 52(3), 561–575. doi:10.1007/s11069-009-9401-4. [1]
-	Kirschbaum, D.B., T. Stanley, Y. Zhou (In press, 2015). Spatial and Temporal Analysis of a Global Landslide Catalog. Geomorphology. doi:10.1016/j.geomorph.2015.03.016. [2]

## Column Data

<table>
<tr>
	<th>Columns 1 - 16</th>
	<th>Columns 17 - 31</th>
	
</tr>
<tr><td>
	
|  Column Name            |  Column Description                      |
|-------------------------|------------------------------------------|
|**source_name**          |News entity                               |
|**source_link**          |News source containing relvent information|
|**event_id**             |Unique id assigned to an event            |
|**event_date**           |Date the event occurred                   |
|**event_time**           |Time the event occurred                   |
|**event_title**          |Title of the news story                   |
|**event_description**    |Description of the event                  |
|**location_description** |Description of the location of the event  |
|**location_accuracy**    |Range in which the location is accurate   |
|**landslide_category**   |Type of landslide event                   |
|**landslide_trigger**    |Cause of landslide event                  |
|**landslide_size**       |Magnitude of the event                    |
|**landslide_setting**    |Environment where the event occurred      |
|**fatality_count**       |Number of deaths due to the event         |
|**injury_count**         |Number of injuries due to the event       |
|**storm_name**           |Name of storm associated with event       |

</td><td>
	
|  Column Name                 |  Column Description                       |
|------------------------------|-------------------------------------------|
|**photo_link**                |Link to photo of event                     |
|**notes**                     |Notes regarding the event record           |
|**event_import_source**       |Source of the event import                 |
|**event_import_id**           |Id of the event import                     |
|**country_name**              |Name of country where event occurred       |
|**country_code**              |Code of country where event occurred       |
|**admin_division_name**       |Name of admin division where event occurred|
|**admin_division_population** |Population of admin division               |
|**gazeteer_closest_point**    |Closest gazeteer point                     |
|**gazeteer_distance**         |Distance from gazeteer point to the event  |
|**submitted_date**            |Date the event was submitted               |
|**created_date**              |Date the event was created                 |
|**last_edited_date**          |Date the record was last edited            |
|**longitude**                 |Longitude of landslide event               |
|**latitude**                  |Latitude of landslide event                |

</td></tr>
</table>


---

# Data Cleaning
**Goals of Data Cleaning** <br>
1. Find and Delete Any Duplicates
2. Standardize and Reformat Columns
3. Find and Populate Null Values
4. Delete Unused Columns
5. Creating Columns

---

## Finding and Deleting Duplicates
Finding and deleting duplicates was accomplished by navigating to the Data tab in Excel and choosing 'Remove Duplicates', ensuring that the box was checked to indicate that the data table had headers.

|Finding Duplicates|No Duplicates Found|
|---|---|
| ![image](https://github.com/user-attachments/assets/d67fbf67-0bff-4a0e-a423-a857f0214d05) | ![image](https://github.com/user-attachments/assets/952f998c-b903-47c4-bbef-f1428d61fa85)|

---

## Finding Null Values
There are 'unknown' and null records in multiple columns within the dataset. The =COUNTBLANK() function was used to count the number of nulls in each column, and the =COUNTIF() function was used to count the number of 'unknown' values in each column (A -  AE).

| |  |
|---|---|
| **Counting Blank Values:** <br> ```=COUNTBLANK(A2:A11034)``` <br> <br> <br> **Counting 'unknown' Values:** <br> ```=COUNTIF(A2:A11034, "unknown")```   |![image](https://github.com/user-attachments/assets/e364d180-bf19-48af-a238-603685cfaea8) |

<br>
The 'event_time' column has 11,033 nulls; however, the event times are located in the 'event_date' column. This column will be used to populate the 'event_time' column.

---

## Reformatting Columns
### Populating event_time
The 'event_date' column is formatted *mm/dd/yyyy hh:mm:ss AM/PM* and will be used to populate the 'event_time' column by utilizing Text-to-Columns.


| | | | 
|---|---|---|
|Original Data Type: Fixed Width | Move break line | Skip import for date column, import time into event_time column |
| ![Screenshot 2025-02-27 161237](https://github.com/user-attachments/assets/9fc68b68-e949-40d9-8c55-3a9d5b436944) | ![image](https://github.com/user-attachments/assets/4cdfe312-58c2-441e-a476-d181bd0bdb1f) | ![image](https://github.com/user-attachments/assets/d7d01db7-36a4-4508-9f14-f84c283ded41) |

<br> 

### Reformatting Columns
Now, the 'event_date' column is reformatted from *mm/dd/yyyy hh:mm:ss AM/PM* to *mm/dd/yyyy*, and the 'event_time' column is reformatted from *hh:mm:ss AM/PM* to *h:mm*.

| | | | 
|---|---|---|
|Event Date | Event Time | Outputs |
| ![image](https://github.com/user-attachments/assets/f55b4bc9-7bfa-41a6-8a91-ef3863d69147) | ![image](https://github.com/user-attachments/assets/05e982ba-9d9d-4ac0-9670-e8065174cd7f) | ![image](https://github.com/user-attachments/assets/9a377954-d0d0-42e1-88f8-744989a3cbb5) |

---

## Populating Columns
Nulls and unknowns are populated using filtering and conditional formatting. Columns that will be populated include, lanslide_trigger, country_name, and admin_division_name

|Populated Columns | Initial Nulls | Populated Nulls | Explanation |
|---|---|---|---|
| **landslide_trigger** | 23 nulls, 1691 unknowns | 8 nulls, 2 unknowns | The 'event_description' is used to populate the null values. The 'storm_name' column also allowed to populate the unknown values. |
| **country_name** | 1,562 | 1,562 |Often, the 'location_description' and 'event_title' columns contain the admin_division_names or country names which could then be be used to populate the 'country' column. Further, sorting the countries by 'latitude' and 'longitude' columns allows further population of the country column. |
| **admin_division_name** | 1,637 | 1,637 | By filtering each country, the 'admin_division_name' can be found in the 'event_title' and 'location_description' columns. Admin division can occasionally be determined using ranges of latitudes and longitudes. |

---

## Deleting Columns
Some columns are either unable to be populated or are unnecessary for analysis. The following columns are deleted from the dataset.
- **source_name**: not necessary for analysis 
- **source_link**: not necessary for analysis 
- **event_title**: not necessary for analysis 
- **event_description**: not necessary for analysis 
- **location_description**: not necessary for analysis 
- **location_accuracy**: not necessary for analysis 
- **storm_name**: not necessary for analysis 
- **photo_link**: not necessary for analysis 
- **notes**: not necessary for analysis 
- **event_import_source**: not necessary for analysis 
- **event_import_id**: not necessary for analysis 
- **country_code**: not necessary for analysis 
- **admin_division_population**: not necessary for analysis 
- **gazeteer_closest_point**: not necessary for analysis 
- **gazeteer_distance**: not necessary for analysis 
- **submitted_date**: not necessary for analysis 
- **created_date**: not necessary for analysis 
- **last_edited_date**: not necessary for analysis 
- **landslide_category**: 69% of column data is comprised of the value 'landslide' - requires greater specificity to consider analyzing 
- **landslide_setting**: 57% of column data contains either null or unknown values  
- **injury_count**: 50% of column data contains nulls 

---

## Deleting Rows
Nulls remain in the 'landslide_trigger', 'landslide_size', and 'fatality_count' columns. These records are either deleted or repopulated with 'NULL', as these columns are used in the exploration, analysis, and visualizations.

|Column Name | Count of Nulls | Explanation |
|---|---|---|
| landslide_trigger | 15 | The rows containing the 15 nulls are deleted, as these rows contain less than 1% of the data in the table and will not greatly impact analysis. |
| landslide_size | 9 | The rows containing the 9 nulls are deleted, as these rows contain less than 1% of the data in the table and will not greatly impact analysis. |
| fatality_count |  1385 | These records are populated with the value 'NULL' to ensure they are not factored into later calculations. |

<br>

When filtering the data, it's discovered that there are 45 rows of data that date before 2007. These rows are deleted to obtain a more accurate annual landslide analysis.

---

## Adding Columns
The column 'event_year' is added to easily analyze landslide data.  This is accomplished using the following function:

```
=YEAR(event_date)
```
---

# Data Exlporation

## Event Time Frame
This dataset observes landslide events between 2007 - 2017. 
- The earliest recorded landslide in this dataset was on 01/02/2007, and the most recent event occurred on 09/28/2017. 
- The greatest number of landslide events during one year occurred in 2010 with 1536 recorded events.
- There were an average of 997 landslide events per year.

| Outputs | Functions |
|---|---|
| ![image](https://github.com/user-attachments/assets/b0e83333-6858-418b-9807-da20fc04181a) | ![image](https://github.com/user-attachments/assets/32b038de-0925-4c95-b0ad-b1c5ba3cc18f) |
| ![image](https://github.com/user-attachments/assets/f04301a0-0538-4cea-8eac-15a70a2561a8) | ![image](https://github.com/user-attachments/assets/20a63c69-22c2-4a52-89a6-a2cbb167c672) |
| ![image](https://github.com/user-attachments/assets/1a33af4a-4d63-4e4b-b543-89ff6660ca5a) | ![image](https://github.com/user-attachments/assets/1ec98db6-d42b-48fd-b51e-efa003e55ff9) |

## Landslide Events by Country
### Country Count
- There are 145 countries included in this datasest

| Outputs | Functions |
|---|---|
| ![image](https://github.com/user-attachments/assets/29d14c4b-ae3c-44fc-8fe4-306aaec6bac0) | ![image](https://github.com/user-attachments/assets/97ceef02-639f-407f-a82b-28ab79d80ce1) |

### Top 5 Countries with the Most Landslide Events
Pivot tables are used to determine the countries with the greatest total number of recorded landslide events.

![image](https://github.com/user-attachments/assets/bd44461a-424a-44bf-8a87-ea3be597c199)

## Landslide Triggers
Landslide events appear to be most often triggered by precipitation events. The five most and least common landslide event triggers are outlined in the following pivot tables. 

| Most Common Triggers | Least Common Triggers |
|---|---|
| ![image](https://github.com/user-attachments/assets/918a57df-8dec-4ccb-a023-8c5457f1f92b) | ![image](https://github.com/user-attachments/assets/f20a59c2-4ba0-4125-9965-0d4b85926a66) |

## Landslide Sizes
The sizes of landslide events are categorized into one of six classifications. Medium-sized events occurred most frequently, while catastrophic-sized events occurred least frequently.

![image](https://github.com/user-attachments/assets/09a2a7ff-b3a2-49eb-8bd8-f87902013e2e)

## Fatality Count
In this dataset, there were a total of 30,622 recorded fatalities due to landslide events between 2007 - 2017. There was an average fatality count of 3.2 persons per landslide event.

| Outputs | Functions |
|---|---|
| ![image](https://github.com/user-attachments/assets/3d820208-a735-40ca-b98f-ea536a205592) | ![image](https://github.com/user-attachments/assets/9e7720a1-aa14-40ea-aeb0-440c3bef3acb) |
| ![image](https://github.com/user-attachments/assets/eca58833-2c28-43e2-a091-ca90f4fa4407) | ![image](https://github.com/user-attachments/assets/46725bef-c71e-4ca6-acb9-5b481c5da8e0) |

The top 10 countries with the highest and lowest average fatality count per event are outlined in the following pivot tables. 

| Top 10 Countries - Highest Average Fatality Count Per Event | Top 10 Countries - Lowest Average Fatality Count Per Event |
|---|---|
| ![image](https://github.com/user-attachments/assets/e6cb8f77-ee07-4bbf-8ede-9a824aa08c85) | ![image](https://github.com/user-attachments/assets/4e8e84df-b621-4a1f-8ef6-061701d3bc31) |

When observing only countries with greater that 10 landslide events between 2007 – 2017, the top 10 countries with the highest average fatality count per landslide event were:

| Top 10 Countries - Highest Average Fatality Count Per Event | Top 10 Countries - Lowest Average Fatality Count Per Event |
|---|---|
| ![image](https://github.com/user-attachments/assets/f1c1a74c-c7d7-4adf-86f1-8b093c3ee2ca) | ![image](https://github.com/user-attachments/assets/156c16ff-bd6d-4244-b799-cd4c9547041f) |

---

# Data Visualizations

Visualizations for this analysis project were completed in Tableau.
[Click here to view the complete Tableau Dashboard](https://public.tableau.com/views/GlobalLandslideData2007-2017_17389771779150/EventsByCountry?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
