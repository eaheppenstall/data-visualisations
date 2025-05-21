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

Next, I reviewed how many columns were partially complete, with a view to removing columns that would not be useful for analysis. I found that the _courses_ and _social_groups_ columns were completely empty, so they could be excluded from the cleaned dataframe. I also decided to delete the _patents_, _about_me_, _also_viewed_, _cover_image_url_, _image_url_, _recommendations_, _related_courses_, _similar_names_, _social_url_, _websites_, _publications_ and _projects columns_, as they were either mostly unpopulated or not useful for analysis.

The dataframe with columns removed is referred to as df_cleaned.

I then observed that 4 columns (_certifications_, _education_, _experience_, and _working_for_ contained lists of dictionaries. The list of dictionaries need to be separated to allow for data analysis and visualisation. 

### 3.1 Writing a function to expand a column containing lists of dictionaries into multiple columns<a name="sec3p1"></a>

This function is applied to each column that has been identified as containing a list of dictionaries. It runs through each row in the defined column and identifies if the cell contains a list. If the cell does, the function loops through the the first 5 key-value pairs and for each key-value pair creates a flat dictionary (expanded_dict[col_name]) where the key is the name of the column (col_name) and the value is the cell entry. This flat dictionary is stored in a flattened list (expanded_rows), which is then converted into a new dataframe (expanded_df). The column that has been expanded is removed from the cleaned dataframe (df_cleaned) to create df_cleaned_1. expanded_df is combined with df_cleaned_1 to create a final dataframe, df_updated.

This function was then applied to the _certifications_, _education_, _experience_, and _working_for_ columns. The output of each was reviewed to see if any columns could be removed. 

**up tp here**
**certifications 2, 3 and 4 are unecessary**

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
