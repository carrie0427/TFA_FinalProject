# TFA_FinalProject

## Group Name ##
All-A+<br /><br />

## Group Member ##
Jiali Fan&emsp;jf3362<br />
Siyao Mi&emsp;sm4935<br /><br />

## Section ##
002<br /><br />

## Description ##

There are two ipynb files included in this project.<br /><br />

### Top10.ipynb ###
First of all, we import csv and pandas for later use. 
```
import pandas as pd
import csv
```
<br />

Then we read the csv file given and use dataframe to contain the data of our chosen zipcode.
```
df = pd.read_csv("311_Service_Requests_2020.csv")
my_zip = df[df["Incident Zip"] == 10036]
```
<br />

The next step is to group the data based on their "Complaint Type". We use `value_counts()` combined with `head()` to calculate the top 10 types of incidents in our neighborhood. `value_counts()` will return a Series in descending order by nature.
```
top10 = my_zip["Complaint Type"].value_counts().head(10)
top10.name = "Total number of incidents"
top10.index.name = "Incident type"
```
<br />

At last, we rename the name to "Total number of incidents" and the index to "Incident type" just for better understanding.
```
top10.name = "Total number of incidents"
top10.index.name = "Incident type"
```
<br />

**Validation:**
We would like to test if the type of top10 is `pandas.Series`.<br />
```
assert isinstance(top10, pd.Series)
```
No AssertionError is raised. So we could assume that the requirements are fulfilled.
<br />
<br />

### Parking.ipynb ###
Like what we have done for the other file, we import csv and pandas for later use. 
```
import pandas as pd
import csv
```
<br />

Also, we read the csv file given and use dataframe to contain the data of our chosen zipcode.
```
df = pd.read_csv("311_Service_Requests_2020.csv")
my_zip = df[df["Incident Zip"] == 10036]
```
<br />

The next step is to compute the number of parking incidents in our ZIP and across all ZIP codes, and the total number of all incidents in our ZIP and across all ZIP codes as well. We use `sum()` to calculate the number of parking incidents and `len()` to get the total number of all incidents.
```
total_number_of_parking_incidents_in_my_ZIP = (my_zip["Complaint Type"] == "Illegal Parking").sum()
total_number_of_all_incidents_in_my_ZIP = len(my_zip)

total_number_of_parking_incidents = (df["Complaint Type"] == "Illegal Parking").sum()
total_number_of_all_incidents = len(df)
```
<br />

After that, we calculate the two proportion by simply using `/`.
```
parking_proportion_in_my_zip = total_number_of_parking_incidents_in_my_ZIP / total_number_of_all_incidents_in_my_ZIP
parking_proportion_of_all = total_number_of_parking_incidents / total_number_of_all_incidents
```
<br />

At last, we assign the boolean of whether the proportion in our neighborhood is greater to that across all ZIP codes to `higher_parking_proportion`.
```
higher_parking_proportion = parking_proportion_in_my_zip > parking_proportion_of_all
```
<br />

In our chosen neightborhood `10036`, the result is `False`, indicating that our ZIP contains a lower proportion of parking incidents than the global value.