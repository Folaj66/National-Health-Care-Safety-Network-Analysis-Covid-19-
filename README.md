# National-Health-Care-Safety-Network-Analysis-Covid-19

![](Covid19Images.jpg)
---

## Introduction
The goal of this project is to perform a comprehensive analysis of the COVID-19 National
Healthcare Safety Network (NHSN) data. The data is available in four zip files representing the
years 2020, 2021, 2022, and 2023.

## Objectives
1. Extract and import the data from the zip files into a SQL database
2. Clean and transform the data to ensure consistency and accuracy
3. Conduct exploratory data analysis to identify trends, patterns, and insights
4. Perform statistical analysis to understand the impact of COVID-19 on healthcare facilities.
5. Generate meaningful visualizations and reports to present the findings to stakeholders.
6. Identify potential areas for improvement in healthcare practices based on the analysis

**_Note_** _The analysis and visualization is Completed with Microsoft Excel and PostgreSQL_

## Questions 
1. Which healthcare facilities had the highest average number of daily COVID-19 cases in
2021? Display the top 10 facilities.
2. Calculate the 7-day moving average of new COVID-19 cases for each healthcare facility.
Which facility had the highest peak in the moving average?
3. Determine the total number of COVID-19 cases, deaths, and recoveries for each state.
Include the state's name and the corresponding counts in the result.
4. Find the top 5 states with the highest mortality rate (deaths per COVID-19 case) in 2022.
5. Identify the healthcare facilities that experienced a significant increase in COVID-19
cases from 2020 to 2021 (more than 50% increase). Display the facility names and the
percentage increase.
6. What is the total number of COVID-19 cases, deaths, and recoveries recorded in the
dataset?
7. Find the healthcare facilities that had a consistent increase in COVID-19 cases for at
least 5 consecutive months. Display the facility names and the corresponding months.
8. Calculate the mortality rate (deaths per COVID-19 case) for each healthcare facility.
9. Are there any significant differences in COVID-19 outcomes based on the type of
healthcare facility (e.g., hospital, nursing home)?
10. How has the number of COVID-19 cases evolved over time (monthly or quarterly)?
11. What is the distribution of healthcare facilities by state?

## Dataset
You can access the Dataset [here](https://download.cms.gov/covid_nhsn/faclevel_2020.zip) 
[2021Dataset](https://download.cms.gov/covid_nhsn/faclevel_2021.zip)
[2022Dataset](https://download.cms.gov/covid_nhsn/faclevel_2022.zip)
[2023Dataset](https://download.cms.gov/covid_nhsn/faclevel_2023.zip)

## Data Cleaning
The Data was firstly imported into Microsoft Excel to normalize the date and to check out each column Data type is correct 
Then the data was saved as a csv(comma seperated version) file and then it was imported into PstgreSQL for Further cleaning and Data Exploration

## Table Creation
An sql query was written to create table for the 4 dataset, Find Below

CREATE TABLE covid2023 
(
    week_ending date,
	provider_name text,
	provider_address text,
	provider_city text,
	provider_state text,
	county text,
	submitted_data text,
	passed_quality_assurance_check text,
	residents_weekly_admissions_covid19 numeric,
	residents_total_admission_covid19 numeric,
	residents_weekly_confirmed_covid19 numeric,
	residents_total_confirmed_covid19 numeric,
	residents_weekly_all_deaths numeric,
	residents_total_all_deaths numeric,
	residents_weekly_covid19_deaths numeric,
	residents_total_covid19_deaths numeric,
	no_of_all_beds numeric,
	total_number_of_occupied_space numeric,
	staff_weekly_confirmed_covid19 numeric,
	staff_total_confirmed_covid19 numeric,
	staff_wekly_covid19_deaths numeric,
	staff_total_covid19_deaths numeric,
    shortage_of_nursing_staff text,
    shortage_of_clinical_staff text,
    shortage_of_aides text,
    shortage_of_other_staff text,
    weekly_resident_confirmed_covid19_cases_per_1000_residents numeric,
    weekly_resident_covid19_deaths_per_1000_residents numeric,
    total_resident_confirmed_covid19_cases_per_1000_residents numeric,
    total_resident_covid19_deaths_per_1000_residents numeric,
    three_or_more_confirmed_covid19_cases_this_week text,
    initial_confirmed_covid19_case_this_week text,
    no_of_resident_with_new_positive_covid19_test_result numeric,
    no_of_resident_with_new_influenza numeric,
    no_of_staffs_and_personnel_with_positive_covid19_test_result numeric,
    no_of_staffs_and_personnel_with_a_new_influenza numeric
	
)

## Further Data Cleaning in PostgreSQL
Steps to be taken to clean this data
1. Update the provider_state column to be full written for all the tables
2. Change the case of all the columns to proper case for all the tables
3. Check for Empty and Null Values */

-- 1. Update the provider_state for the column covid2020, covid2021, covid2022, covid2023

UPDATE covid2020
SET provider_state = 
    CASE 
        WHEN provider_state = 'AL' THEN 'ALABAMA'
        WHEN provider_state = 'AK' THEN 'ALASKA'
        WHEN provider_state = 'AZ' THEN 'ARIZONA'
		WHEN provider_state = 'AR' THEN 'Arkansas'
		WHEN provider_state = 'CA' THEN 'CALIFORNIA'
		WHEN provider_state = 'CO' THEN 'COLORADO'
		WHEN provider_state = 'CT' THEN 'CONNETICUT'
		WHEN provider_state = 'DE' THEN 'DELAWARE'
		WHEN provider_state = 'DC' THEN 'DISTRICT OF COLUMBIA'
		WHEN provider_state = 'FL' THEN 'FLORIDA'
		WHEN provider_state = 'GA' THEN 'GEORGIA'
		WHEN provider_state = 'GU' THEN 'GUAM'
		WHEN provider_state = 'HI' THEN 'HAWAII'
		WHEN provider_state = 'ID' THEN 'IDAHO'
		WHEN provider_state = 'IL' THEN 'ILLINOIS'
		WHEN provider_state = 'IA' THEN 'IOWA'
		WHEN provider_state = 'IN' THEN 'INDIANA'
		WHEN provider_state = 'KS' THEN 'KANSAS'
		WHEN provider_state = 'KY' THEN 'KENTUCKY'
		WHEN provider_state = 'LA' THEN 'LOUISIANA'
		WHEN provider_state = 'ME' THEN 'MAINE'
		WHEN provider_state = 'MD' THEN 'MARYLAND'
		WHEN provider_state = 'MA' THEN 'MASSACHUSETTS'
		WHEN provider_state = 'MI' THEN 'MICHIGAN'
		WHEN provider_state = 'MN' THEN 'MINNESOTA'
		WHEN provider_state = 'MS' THEN 'MISSISSIPPI'
		WHEN provider_state = 'MO' THEN 'MISSOURI'
		WHEN provider_state = 'MT' THEN 'MONTANA'
		WHEN provider_state = 'NE' THEN 'NEBRASKA'
		WHEN provider_state = 'NV' THEN 'NEVADA'
		WHEN provider_state = 'NH' THEN 'NEW HAMPSHIRE'
		WHEN provider_state = 'NJ' THEN 'NEW JERSEY'
		WHEN provider_state = 'NM' THEN 'NEW MEXICO'
		WHEN provider_state = 'NY' THEN 'NEW YORK'
		WHEN provider_state = 'NC' THEN 'NORTH CAROLINA'
		WHEN provider_state = 'ND' THEN 'NORTH DAKOTA'
		WHEN provider_state = 'OH' THEN 'OHIO'
		WHEN provider_state = 'OK' THEN 'OKLAHOMA'
		WHEN provider_state = 'OR' THEN 'OREGON'
		WHEN provider_state = 'PA' THEN 'PENNYSYLVANIA'
		WHEN provider_state = 'PR' THEN 'PUERTO RICO'
		WHEN provider_state = 'RI' THEN 'RHODE ISLAND'
		WHEN provider_state = 'SC' THEN 'SOUTH CAROLINA'
		WHEN provider_state = 'SD' THEN 'SOUTH DAKOTA'
		WHEN provider_state = 'TN' THEN 'TENNESSEE'
		WHEN provider_state = 'TX' THEN 'TEXAS'
		WHEN provider_state = 'UT' THEN 'UTAH'
		WHEN provider_state = 'VT' THEN 'VERMONT'
		WHEN provider_state = 'VA' THEN 'VIRGINIA'
		WHEN provider_state = 'WA' THEN 'WASHINGTON'
		WHEN provider_state = 'WV' THEN 'WEST VIRGINIA'
		WHEN provider_state = 'WI' THEN 'WISCONSIN'
		WHEN provider_state = 'WY' THEN 'WYOMING'
		ELSE provider_state
    END;
--2. change case of all the columns for each tables
--covid2020, covid2021, covid2022, covid2023

UPDATE covid2023
SET
    provider_name = initcap(provider_name),
	provider_address = initcap(provider_address),
	provider_city = initcap(provider_city),
	provider_state = initcap(provider_state),
	county = initcap(county),
	submitted_data = initcap(submitted_data),
	passed_quality_assurance_check = initcap(passed_quality_assurance_check),
	shortage_of_nursing_staff = initcap(shortage_of_nursing_staff),
	shortage_of_clinical_staff = initcap(shortage_of_clinical_staff),
	shortage_of_aides = initcap(shortage_of_aides),
	shortage_of_other_staff = initcap(shortage_of_other_staff),
	three_or_more_confirmed_covid19_cases_this_week = initcap(three_or_more_confirmed_covid19_cases_this_week),
	initial_confirmed_covid19_case_this_week = initcap(initial_confirmed_covid19_case_this_week);
