# DATA-1202-FINAL-ASSIGNMENT-ID-100801304-

****PROJECT OVERVIEW****

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

**FULL SQL CODE WITH OUTPUT SNAPSHOTS**
```sql
-- Extraction along with data cleaning and quality check: Count missing values in patient health and diet table --
SELECT COUNT(*) AS MissingValues
FROM healthdata.`patient health and diet`
WHERE Heart_Disease IS NULL
   OR Skin_Cancer IS NULL
   OR Other_Cancer IS NULL
   OR Depression IS NULL
   OR Diabetes IS NULL
   OR Arthritis IS NULL
   OR Smoking_History IS NULL
   OR Alcohol_Consumption IS NULL
   OR Fruit_Consumption IS NULL
   OR Green_Vegetables_Consumption IS NULL
   OR FriedPotato_Consumption IS NULL;
```
**OUTPUT**
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/9fb4e705-5920-4e84-a390-c941b5eea305)

```sql
-- Extraction along with data cleaning and quality check: Count missing values in patient profile table --
SELECT COUNT(*) AS MissingValues
FROM healthdata.`patient profile`
WHERE General_Health IS NULL
   OR Checkup IS NULL
   OR Exercise IS NULL
   OR Sex IS NULL
   OR Age_Category IS NULL
   OR `Height_(cm)` IS NULL
   OR `Weight_(kg)` IS NULL
   OR BMI IS NULL;
```
**OUTPUT**
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/7f922dab-29d4-4ea0-949d-0752a8726119)

```sql
-- Transformation: Heart Disease Distribution and Exercise Habits Analysis --
SELECT pp.Exercise, phd.Heart_Disease, COUNT(*) AS Count
FROM healthdata.`patient health and diet` phd
JOIN healthdata.`patient profile` pp ON phd.ID = pp.ID
GROUP BY pp.Exercise, phd.Heart_Disease
ORDER BY pp.Exercise, phd.Heart_Disease;
```
**OUTPUT**
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/d5e2c3a7-0543-431f-b15a-ad2b2497330f)
```sql
-- Transformation: Average BMI by Age Category --
SELECT
    p.Age_Category,
    AVG(p.BMI) AS Average_BMI
FROM
    healthdata.`patient profile` p
GROUP BY
    p.Age_Category
ORDER BY
    p.Age_Category;
```
**OUTPUT**
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/8c81d9fa-b497-4bb4-854a-f03f804a0779)

```sql
-- Transformation: Gender-based Health Patterns --
SELECT
    p.Sex,
    AVG(CASE WHEN hd.Heart_Disease = 'Yes' THEN 1 ELSE 0 END) AS Heart_Disease_Rate,
    AVG(CASE WHEN hd.Skin_Cancer = 'Yes' THEN 1 ELSE 0 END) AS Skin_Cancer_Rate,
    AVG(CASE WHEN hd.Other_Cancer = 'Yes' THEN 1 ELSE 0 END) AS Other_Cancer_Rate,
    AVG(CASE WHEN hd.Depression = 'Yes' THEN 1 ELSE 0 END) AS Depression_Rate,
    AVG(CASE WHEN hd.Diabetes = 'Yes' THEN 1 ELSE 0 END) AS Diabetes_Rate,
    AVG(CASE WHEN hd.Arthritis = 'Yes' THEN 1 ELSE 0 END) AS Arthritis_Rate
FROM
    healthdata.`patient health and diet` hd
JOIN
    healthdata.`patient profile` p ON hd.ID = p.ID
GROUP BY
    p.Sex
ORDER BY
    p.Sex;
```
**OUTPUT**
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/a1d0cbf4-0083-4186-966c-d32a71d2fad0)

```sql
-- Transformation: Nutrition Habits and Health Conditions --
SELECT
    AVG(CASE WHEN hd.Heart_Disease = 'Yes' THEN 1 ELSE 0 END) AS Heart_Disease_Rate,
    AVG(CASE WHEN hd.Skin_Cancer = 'Yes' THEN 1 ELSE 0 END) AS Skin_Cancer_Rate,
    AVG(CASE WHEN hd.Other_Cancer = 'Yes' THEN 1 ELSE 0 END) AS Other_Cancer_Rate,
    AVG(CASE WHEN hd.Depression = 'Yes' THEN 1 ELSE 0 END) AS Depression_Rate,
    AVG(CASE WHEN hd.Diabetes = 'Yes' THEN 1 ELSE 0 END) AS Diabetes_Rate,
    AVG(CASE WHEN hd.Arthritis = 'Yes' THEN 1 ELSE 0 END) AS Arthritis_Rate,
    AVG(CASE WHEN hd.Fruit_Consumption = 'Yes' THEN 1 ELSE 0 END) AS High_Fruit_Consumption_Rate,
    AVG(CASE WHEN hd.Green_Vegetables_Consumption = 'Yes' THEN 1 ELSE 0 END) AS High_Green_Vegetables_Consumption_Rate,
    AVG(CASE WHEN hd.FriedPotato_Consumption = 'No' THEN 1 ELSE 0 END) AS Low_FriedPotato_Consumption_Rate
FROM
    healthdata.`patient health and diet` hd
JOIN
    healthdata.`patient profile` p ON hd.ID = p.ID;
```
**OUTPUT**
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/997d428e-a686-49f9-8157-ddee40c6a096)

```sql
-- Transformation: Average BMI by General Health Status --
SELECT
    p.General_Health,
    ROUND(AVG(p.BMI)) AS Average_BMI
FROM
    healthdata.`patient profile` p
GROUP BY
    p.General_Health;
```
**OUTPUT**
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/d32816d5-47e7-4ed4-99bc-ab122fb40e02)

```sql
-- Transformation: CHECK DATA TYPES --
SELECT COLUMN_NAME, DATA_TYPE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_SCHEMA = 'healthdata'
  AND TABLE_NAME IN ('patient health and diet', 'patient profile');    
```
**OUTPUT**
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/6b82e51c-0de3-4aee-9dff-0ad609bbfba3)
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/1dbf0df4-d585-4bc4-bf2d-be1fe89d074a)

```sql
-- Loading along with data cleaning and quality check: GENERAL AGE_GENDER_HEALTH_INSIGHTS -- 
CREATE TABLE AGE_GENDER_HEALTH_INSIGHTS AS (
    SELECT
        p.Age_Category,
        p.Sex,
        MAX(p.General_Health) AS General_Health,
        MAX(p.Checkup) AS General_Checkup_Status,
        MAX(pp.Exercise) AS General_Exercise_Rate,
        ROUND(AVG(CASE WHEN p.BMI REGEXP '^[0-9]*\\.?[0-9]+$' THEN CAST(p.BMI AS DOUBLE) ELSE NULL END), 2) AS Avg_BMI,
        AVG(CASE WHEN hd.Heart_Disease = 'Yes' THEN 1 ELSE 0 END) AS Heart_Disease_Rate,
        AVG(CASE WHEN hd.Skin_Cancer = 'Yes' THEN 1 ELSE 0 END) AS Skin_Cancer_Rate,
        AVG(CASE WHEN hd.Other_Cancer = 'Yes' THEN 1 ELSE 0 END) AS Other_Cancer_Rate,
        AVG(CASE WHEN hd.Depression = 'Yes' THEN 1 ELSE 0 END) AS Depression_Rate,
        AVG(CASE WHEN hd.Diabetes = 'Yes' THEN 1 ELSE 0 END) AS Diabetes_Rate,
        AVG(CASE WHEN hd.Arthritis = 'Yes' THEN 1 ELSE 0 END) AS Arthritis_Rate,
        AVG(CASE WHEN hd.Smoking_History = 'Yes' THEN 1 ELSE 0 END) AS Smoking_History_Rate,
        AVG(hd.Alcohol_Consumption) AS Average_Alcohol_Consumption,
        AVG(hd.Fruit_Consumption) AS Average_Fruit_Consumption,
        AVG(hd.Green_Vegetables_Consumption) AS Average_Green_Vegetables_Consumption,
        AVG(hd.FriedPotato_Consumption) AS Average_FriedPotato_Consumption
    FROM healthdata.`patient profile` p
    LEFT JOIN healthdata.`patient health and diet` hd ON p.ID = hd.ID
    LEFT JOIN healthdata.`patient profile` pp ON p.Age_Category = pp.Age_Category AND p.Sex = pp.Sex
    GROUP BY
        p.Age_Category,
        p.Sex
    ORDER BY
        CASE
            WHEN p.Age_Category = '18-24' THEN 1
            WHEN p.Age_Category = '25-29' THEN 2
            WHEN p.Age_Category = '30-34' THEN 3
            WHEN p.Age_Category = '35-39' THEN 4
            WHEN p.Age_Category = '40-44' THEN 5
            WHEN p.Age_Category = '45-49' THEN 6
            WHEN p.Age_Category = '50-54' THEN 7
            WHEN p.Age_Category = '55-59' THEN 8
            WHEN p.Age_Category = '60-64' THEN 9
            WHEN p.Age_Category = '65-69' THEN 10
            WHEN p.Age_Category = '70-74' THEN 11
            WHEN p.Age_Category = '75-79' THEN 12
            WHEN p.Age_Category = '80+' THEN 13
        END,
        p.Sex
);
```
**OUTPUT**
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/a3d69ff4-c9c1-441a-94ca-1e6c1a6930b9)

```sql
-- Loading: View to Get Average BMI by Age Category --
CREATE VIEW Avg_BMI_By_Age AS
SELECT Age_Category, Avg_BMI
FROM AGE_GENDER_HEALTH_INSIGHTS
GROUP BY Age_Category, Avg_BMI;
```
**OUTPUT**
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/10260ebf-37bd-46fd-825e-81443d66a010)

```sql
-- Loading: View to Get Age-based Depression Rates --
CREATE VIEW Age_Depression_Rates AS
SELECT Age_Category, Depression_Rate
FROM AGE_GENDER_HEALTH_INSIGHTS
GROUP BY Age_Category, Depression_Rate;
```
**OUTPUT**
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/b00ab384-3ee3-4407-8cab-18f2b923f496)

```sql
-- Loading: View to Get Smoking and Alcohol Consumption Patterns --
CREATE VIEW smoking_alcohol_patterns AS
SELECT
    Sex,
    AVG(Smoking_History_Rate) AS Avg_Smoking_History_Rate,
    AVG(Average_Alcohol_Consumption) AS Avg_Average_Alcohol_Consumption
FROM AGE_GENDER_HEALTH_INSIGHTS
GROUP BY Sex;
```
**OUTPUT**
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/dceb704e-530f-4503-9d2a-a5bf914ee301)

```sql
-- Loading: View to Get Nutritional Habits and Health Conditions --
CREATE VIEW Nutrition_Health_Habits AS
SELECT Age_Category, Average_Fruit_Consumption, Average_Green_Vegetables_Consumption,
       Average_FriedPotato_Consumption, Heart_Disease_Rate, Diabetes_Rate, Arthritis_Rate
FROM AGE_GENDER_HEALTH_INSIGHTS
ORDER BY Heart_Disease_Rate DESC, Diabetes_Rate DESC, Arthritis_Rate DESC;
```
**OUTPUT**
![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT/assets/138626409/622a0256-1be3-4b00-aaa7-947a0e56b1a9)

**WHOLE PROCESS EXPLAINED WITH ISSUES FACED,SOLUTIONS AND IMPACTS**

**DATA EXTRACTION:**

Database Setup: Created a new MySQL database named 'healthdata' to store the health-related data.

Data Loading and Table Creation: Utilized the MySQL "Table data import wizard" to load data from the CSV files into the tables named 'patient health and diet' and 'patient profile'.

Data Validation: Performed preliminary data validation during the loading process to identify any irregularities or inconsistencies.

**ISSUES FACED:**

Data Formatting: Encountered issues with inconsistent formatting of certain columns, such as non-numeric characters in BMI.

Null Values: Some columns contained significant null values that needed to be addressed to ensure data integrity.

**SOLUTIONS IMPLEMENTED:**

Data Cleaning: Used SQL functions to remove non-numeric characters from BMI values and converted them to numeric types.

Null Handling: Executed SQL statements to identify and update null values in critical columns based on context or averages.

**SCREENSHOT OF A SELECT STATEMENT DONE:**

![image](https://github.com/VinithaVarghese/DATA-1202-FINAL-ASSIGNMENT-ID-100801304-/assets/138626409/44f0e968-af11-4a7b-8304-79445b2cb7a4)

**DATA TRANSFORMATION**

In the data transformation phase, I conducted quality checks, performed transformations, and employed aggregation and JOIN operations to derive valuable insights from health-related data. Here are the details of the transformations I applied:

**Quality Checks:**

Conducted checks to ensure data consistency, identifying any missing or incomplete values in critical columns like Heart_Disease, Skin_Cancer, etc.
Verified data types to ensure correct numeric and string formats.

**Aggregation and JOIN Operations:**

**Heart Disease Distribution and Exercise Habits Analysis:**
Aggregated data by joining the 'patient health and diet' table with the 'patient profile' table using the 'ID' column. This allowed me to analyze the relationship between exercise habits, heart disease, and their distribution.

**Average BMI by Age Category:**
Utilized a GROUP BY operation on the 'Age_Category' column in the 'patient profile' table to calculate the average BMI for each age category, providing insights into health trends by age.

**Gender-based Health Patterns:**
Employed a JOIN operation between the 'patient health and diet' and 'patient profile' tables using the 'ID' column. By grouping data based on 'Sex', I calculated average rates of various health conditions like Heart Disease, Skin Cancer, etc.

**Nutrition Habits and Health Conditions:**
Used aggregation and JOIN operations to analyze nutrition habits and health conditions, calculating average rates of various health conditions and nutritional habits from both tables.

**Average BMI by General Health Status:**
Aggregated data by 'General_Health' status using the 'patient profile' table, calculating the rounded average BMI for each health status category.

**EFFECTS OF TRANSFORMATIONS:**

**Insightful Analysis:** The applied transformations allowed me to gain valuable insights into the relationships between health conditions, exercise habits, nutrition, and demographic factors such as age and gender.

**Better Decision-Making:** Aggregating and analyzing data through GROUP BY and JOIN operations enabled me to identify patterns and trends, aiding in data-driven decision-making for health-related recommendations and interventions.

**Data Integrity Enhancement:** Addressing missing values and data inconsistencies during quality checks improved the integrity of the data, ensuring accurate analysis and insights.

**Deeper Understanding:** The transformations helped in understanding correlations between different health factors and demographic characteristics, contributing to a more comprehensive view of the dataset.


**DATA LOADING**

In the data loading phase, I loaded the clean and transformed data into a second table named AGE_GENDER_HEALTH_INSIGHTS in the MySQL database. Here's how the process was done and the reasoning behind it:

**LOADING PROCESS:**

During the data loading phase, I incorporated the cleaned and transformed data into a MySQL database by creating views that combine relevant information from various tables. This approach allowed me to avoid duplicating data while enabling efficient analysis through SQL queries. I utilized the CREATE VIEW statement to generate dynamic virtual tables based on the transformed data, ensuring consistent and up-to-date insights without the need to duplicate or store the data redundantly.

**HOW THIS PROCESS WAS DONE:**

**Database Structure and Transformation:**
After performing data cleaning and transformation, I had a set of cleaned and processed tables representing different aspects of health and lifestyle data. These tables were designed to be free of inconsistencies, missing values, and outliers, ensuring the integrity of the data.

**Creating Views:**
Instead of creating new physical tables to store the transformed data, I opted to create views. Views are virtual tables that are defined by SQL queries. They allow users to query and retrieve data just like they would from a regular table. Views don't store data themselves; they simply present the data in a structured format based on the underlying source tables thereby consuming only minimal additional storage space.

I created views using SQL queries that combined data from multiple source tables based on common columns or criteria. For instance, I created a view to calculate average BMI by age category, another view to capture health patterns by gender, and so on.

**THE RATIONALS FOR USING VIEWS**

**Loading Impact:** By using views to load the data, the impact on the database was minimized in terms of storage and maintenance. It helped maintain data integrity and consistency and allowed users to efficiently query and analyze the transformed data without needing to re-run transformations each time.

**Querying:** Analysts and users could easily query the views to extract meaningful insights without dealing with the intricacies of data transformations. The views provided a convenient way to perform various analyses and generate reports.

**Real-time Data:** Views allowed real-time access to the most up-to-date data. Any changes made to the source tables would be immediately reflected in the views.

In summary, the decision to load the cleaned and transformed data through views was motivated by the need for data integrity, performance optimization, data abstraction, and access control. This approach streamlined data access, reduced data duplication, and ensured that the most accurate and up-to-date information was available for analysis tasks.

**REFLECTION:**

Through this project, I've gained practical insights into health data analysis using SQL, encompassing data extraction, transformation, and loading stages. Addressing challenges like data inconsistencies and missing values underscored the importance of thorough data cleaning. Structuring transformation processes effectively with appropriate aggregations and JOINs unveiled valuable patterns and correlations. Future-wise, I'd prioritize exploratory data analysis for better insights upfront and document decisions comprehensively. Overall, this experience has honed my SQL skills, deepened my understanding of data analysis, and underscored the significance of data quality and insightful transformations.

