# DATA-1202-FINAL-ASSIGNMENT-ID-100801304-

**PROJECT EXPLAINED**
**Health Data Analysis Repository**
Welcome to the Health Data Analysis repository! In this project, we perform an in-depth analysis of health and lifestyle data using SQL queries to uncover valuable insights regarding health conditions, exercise habits, and age-gender patterns. The analysis is conducted using two primary datasets: "patient health and diet" and "patient profile."

**DATA SOURCES USED**
The data source for this assignment is downloaded from below link:
**https://www.kaggle.com/datasets/alphiree/cardiovascular-diseases-risk-prediction-dataset**
The dataset is split into a fact table and a dimension table as mentioned below.
**Fact Table**: The fact table used for analysis is the "patient health and diet" dataset. This dataset contains detailed health-related information and dietary habits of patients.
**Dimension Table**: The dimension table used for contextual information is the "patient profile" dataset. This dataset provides essential patient details such as age, gender, and general health.

**PROJECT STEPS**
**Data Preprocessing**: We start by loading and inspecting the datasets. Missing values are handled, and data is cleaned and prepared for analysis.

**Health Patterns Analysis**: Using SQL queries, we perform a variety of analyses to gain insights, including:

Gender-based health patterns
Distribution of heart disease and exercise habits
Average BMI by age category
Nutrition habits and their correlation with health conditions

**Insights Generation**: We derive meaningful insights from the data, such as identifying the gender and age category most prone to heart diseases and depression, along with their exercise habits.

**Creating Views**: Views are created to simplify complex queries and provide useful insights, such as average BMI by age category and smoking-alcohol consumption patterns.

**Insights**
The analysis leads to the following key insights:
The sex most prone to heart diseases is female, and their exercise habit is moderate.
The age group most prone to heart disease is 45-49, and their exercise habit is moderate.
The sex most prone to depression is male, and their exercise habit is low.
The age group most prone to depression is 60-64, and their exercise habit is low.

**Repository Structure**
DATASETS: Contains the raw datasets used for analysis including fact table and dimension table.
SCREENSHOTS: SQL code snippets for analysis stored in text files.
README.md: The file you're currently reading, which provides an overview of the project.
CODE: The scripts used for ETL process.

**How to Run**
To replicate the analysis and generate insights:
Set up your database and load the "patient health and diet" and "patient profile" datasets.
Execute the SQL code snippets provided in the text files within the notebooks directory.
Review the generated insights from the executed SQL queries to gain a comprehensive understanding of the data patterns.

**Technologies Used**
SQL

