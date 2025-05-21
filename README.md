# Data-visualisations
A project to create data visualisations for a client to identify any useful trends.

Git-hub repository at:
https://github.com/eaheppenstall/data-visualisations

- Python file: **[Data Visualisations](ADD LINK HERE)**
- Data set: available upon request: eaheppenstall@gmail.com

# Table of contents
1. [Introduction](#introduction)

2. [Description of the data set](#section2)

3. [Data cleaning](#section3)
    1. [Writing a function to expand a column containing lists of dictionaries into multiple columns](#sec3p1)
    2. [Writing a function to determine if a role change has occurred during the 12 months following the Credential Issue Date](#sec4p2)

4. [Data visualisations](#section4)
    1. [Where are individuals located?](#sec4p1)
    2. [Question 2](#sec4p2)
    3. [Question 3](#sec4p3)

5. [Conclusions](#conclusion)
    
6. [Next steps](#nextsteps)

## 1. Introduction <a name="introduction"></a>
- This README describes how I approached creating visualisations from a set of data. The goal was broad: to identify useful trends or summaries that would be useful for the data owner. Resources used include Python, and associated packages Pandas and Numpy for data cleaning and matplotlib for the visualisations. The analysis can be found at the filename given above.  


##  2. Description of the data set <a name="section2"></a>
The dataset contians public LinkedIn data from around 140 individuals who have been issued an Accredible credential from a specific Accredible customer. The data is stored in a CSV file.

## 3. Data cleaning <a name="section3"></a>

I loaded the data into a Pandas dataframe. All the data is contained in one column in JSON format, so I took steps to extract and flatten the JSON data, before creating a new dataframe with separate columns for each data point. 

Next, I reviewed how many columns were partially complete, with a view to removing columns that would not be useful for analysis. I found that the courses and social_groups columns were completely empty, so they could be excluded from the cleaned dataframe. I also decided to delete the patents, about_me, also_viewed, cover_image_url, image_url, recommendations, related_courses, similar_names, social_url, websites, publications and projects columns, as they were either mostly unpopulated or not useful for analysis.

I then observed that 4 columns (certifications, education, experience, and working_for) contained lists of dictionaries. The list of dictionaries need to be separated to allow for data analysis and visualisation. 

### 3.1 Writing a function to expand a column containing lists of dictionaries into multiple columns<a name="sec3p1"></a>

This function is applied to each column that has been identified as containing a list of dictionaries. It runs through each row in the defined column and identifies if the cell contains a list. If the cell does, the function loops through the the first 5 key-value pairs and for each key-value pair creates a flat dictionary where the key is the name of the column and the value is the cell entry. This flat dictionary is stored in a flattened list, which is then converted into a dataframe. 

aDD NAMES TO THINGS HERE FOR A CLEARER EXPLANATION 

takes the Credential Issue Date as the reference point. It then looks through the role title columns (current role, previous role etc.) to see which role was held on the Credential Issue Date. It then creates a data point in a new column entitled 'role_on_credential_date' which lists the role title held on the Credential Issue Date.

I cleaned the data so that it contained separate columns for current role and previous role entries. Some individuals listed multiple current/previous roles and so each role was given a separate column. Start and end dates for these associated roles were included in most cases. 

74 individuals did not give a start date for their current role and so I changed this to 1 January 2024, which is more than 12 months after the latest credential issue date. This means it won't affect my results, but I don't have to delete the data row.

Some individuals did not give a start date for their previous role and so I changed this to 0 (converts to a timestamp date of 1970-01-01). This is before Accredible started operating, so it shouldn't affect my results and I don't have to delete the data row. 

Some start/end dates are listed as unix timestamps. These have been converted to a human-readable date (not including time)

The dataset looks like: 

![json](https://github.com/eaheppenstall/Impact-of-credential-on-career-development/blob/main/Images/json%20file%20dataset%20screenshot.png)

### 2.1 Initial steps: data cleaning of the json file <a name="sec2p1"></a>
### 2.2 Initial steps: data cleaning of the csv file <a name="sec2p2"></a>

I loaded the data into a Pandas dataframe. As I intended to match the dataframes based on surname, I cleaned the dataframe so that surname was captured as a separate column (rather than being included in a fullname column). 

Credential Issue Dates were converted to a human-readable date.

The dataset looks like: 

![csv](https://github.com/eaheppenstall/Impact-of-credential-on-career-development/blob/main/Images/csv%20file%20dataset%20screenshot.png)

## 4. Writing functions <a name="section4"></a>

### 4.1 Writing a function to determine the job role on the Credential Issue Date <a name="sec4p1"></a>

This function takes the Credential Issue Date as the reference point. It then looks through the role title columns (current role, previous role etc.) to see which role was held on the Credential Issue Date. It then creates a data point in a new column entitled 'role_on_credential_date' which lists the role title held on the Credential Issue Date.

### 4.2 Writing a function to determine if a role change has occurred during the 12 months following the Credential Issue Date <a name="sec4p2"></a>

This function defines the 12 month window for each individual as 12 months after the Credential Issue Date. It then looks to see if a role change has occured within each individual's 12 month window. It returns a list of roles started within the 12 month window, or returns [] where no new role has been started.

## 5. Results <a name="section5"></a>

The main finding of this analysis is that only 21 roles changed within 12 months of the Credential Issue Date

## 6. Conclusion <a name="conclusion"></a>

This analysis found that 14% of job roles changed within 12 months of the Credential Issue Date. I would say that this is not a large enough percentage to say that Accredible had an effect on the job role change and that further analysis is needed to draw more solid conclusions. 

## 7. Next Steps <a name="nextsteps"></a>

Further analysis is needed to test this result against a control set (i.e. a group of individuals who haven't interacted with Accredible. Ideally, the control group would be a group of individuals with similar job roles to that in this dataset. 

It would also be interesting to link salary data here, to see how valuable an Accredible credential is.
