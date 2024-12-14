![image](https://github.com/user-attachments/assets/80b3c562-7841-4327-8ceb-34355431c051)# **Project: Design and Implementation of a Data Analytics Platform for Vancouver**
________________________________________
## **Objective**

The objective of this project was to design and implement a scalable and efficient Data Analytics Platform (DAP) for the City of Vancouver using Amazon Web Services (AWS). The platform aimed to enable data-driven decision-making for urban management, enhance data accessibility, and ensure robust data security, governance, and observability.
________________________________________
## **Dataset**

The project utilized the Street Trees Dataset sourced from the City of Vancouver’s Open Data Portal. This dataset contains comprehensive information about public trees, including:
- Tree Species

-	Planting Dates

-	Geospatial Coordinates (Latitude and Longitude)

-	Tree Dimensions (e.g., Diameter)

-	Neighborhood Information

________________________________________
## **Methodology**

![image](https://github.com/user-attachments/assets/84a2c930-85bf-4358-8eaa-2bb09d6c1ee9)


The project consisted of the following phases:

### **1. Data Ingestion**

![image](https://github.com/user-attachments/assets/f3b3a767-c296-4ca8-967d-f2e52c203ea6)


-	Stored the raw dataset in an Amazon S3 bucket (va-raw-nat), organized by ingestion year (2024).

-	Configured lifecycle rules to transition older data to Amazon S3 Glacier for cost-effective long-term storage.

### **2. Data Profiling**

![image](https://github.com/user-attachments/assets/a3b94e20-862c-4332-9a26-9267cf438590)


-	Conducted profiling using AWS Glue DataBrew to analyze dataset characteristics.

-	Identified:

	 -	Missing values in critical fields (e.g., DATE_PLANTED, DIAMETER).

	 -	Outliers in numerical data.

	 -	Column correlations for potential enrichments.

### **3. Data Cleaning**

![image](https://github.com/user-attachments/assets/fdbb372b-c4cd-4b34-8dc1-c3811d05970b)


-	Addressed missing values and inconsistencies using AWS Glue transformations.

-	Performed:

	-	Standardization of column names and formats.

	-	Removal of invalid or duplicate records.

-	Stored the cleaned dataset in the va-trf-nat S3 bucket.

### **4. Data Enriching**

![image](https://github.com/user-attachments/assets/d93f0094-3c4b-4663-8457-fbd75e7015fb)
	
-	Enhanced the dataset through the following steps:

	-	Tree Age Calculation: Computed tree age using the DATE_PLANTED column.

	-	Carbon Sequestration Estimation: Added a calculated field for carbon sequestration using the DIAMETER and GENUS_NAME columns.

	-	Geospatial Transformation: Split the geo_point_2d column into separate latitude and longitude fields for mapping.

-	Validated the enriched data using Amazon Athena.

-	Stored the enriched dataset in the va-cur-nat S3 bucket.

### **5. Data Security**

-	Ensured data security through:

  -	**Encryption:** Applied server-side encryption (SSE) using AWS KMS with AES-256 for data at rest.

  -	**Secure Transmission:** Enforced HTTPS for data transfer by updating the S3 bucket policy to reject unsecured requests.

  -	**Access Control:** Configured IAM roles with the least privilege principle. Only authorized roles could access specific datasets.

  -	**Cross-Region Replication (CRR):** Enabled replication of the raw dataset to a secondary bucket for disaster recovery.

### **6. Data Governance**

![image](https://github.com/user-attachments/assets/92be1490-7dcb-4796-9472-9f86caca5bbe)


-	Established a governance framework to ensure data quality and compliance:

	-	Completeness: Ensured all critical fields (e.g., DATE_PLANTED, DIAMETER) were non-null.

	-	Freshness: Monitored datasets to ensure updates within a 30-day window.

	-	Validation Rules: Routed valid data to a "Pass Data" folder and invalid records to a "Failed Data" folder for remediation.

	-	Standardization: Applied transformations to align data types with the schema in the Glue Data Catalog.

### **7. Data Observability**

![image](https://github.com/user-attachments/assets/a9bc9af3-d96a-4989-a1f1-1e8d81c37bab)


-	Configured observability tools to monitor pipeline performance and detect anomalies:

	-	Created a CloudWatch Dashboard (tree-dash-nat) to display key metrics:

		-	Bucket storage usage.

		- Glue job execution times and errors.

		- Pipeline costs.

	-	Enabled S3 Access Logs to track interactions with the dataset.

	-	Set up CloudTrail Logs to audit API calls related to S3 and Glue.

	-	Configured alarms to notify of Glue job failures or unusual storage growth.

________________________________________
## **Tools and Technologies**

-	**Data Storage:** Amazon S3 (with lifecycle rules and versioning)

-	**Data Processing:** AWS Glue, AWS DataBrew

-	**Querying and Analysis:** Amazon Athena

-	**Monitoring:** Amazon CloudWatch, AWS CloudTrail

-	**Security:** AWS Key Management Service (KMS)

________________________________________
## **Deliverables**

### **1.	Data Pipeline:**

-	A fully functional pipeline capable of ingesting, cleaning, enriching, and securing urban datasets.

### **2.	Cleaned and Enriched Datasets:**

-	Processed datasets stored in dedicated S3 buckets (va-trf-nat and va-cur-nat).

### **3.	Monitoring Dashboard:**

-	CloudWatch dashboard for real-time pipeline performance monitoring.

### **4.	Governance Framework:**

-	Automated validation and routing of data based on quality checks.

________________________________________
## **Key Insights**

-	The combination of AWS Glue, S3, and Athena enabled efficient and scalable data processing.

-	Encryption and access controls ensured the dataset’s confidentiality and compliance with security standards.

-	Observability tools such as CloudWatch and CloudTrail facilitated proactive issue resolution and cost monitoring.

-	Governance rules ensured data completeness, freshness, and quality, making the dataset reliable for analysis and decision-making.

________________________________________

This project successfully implemented a robust Data Analytics Platform (DAP) using AWS services. By focusing on data security, governance, and observability, the platform provided a scalable, secure, and compliant solution for managing urban datasets. The enriched and validated street trees dataset is now a reliable resource for supporting the City of Vancouver’s urban planning and sustainability initiatives. The project demonstrates expertise in leveraging AWS technologies to deliver end-to-end data solutions, aligning with best practices for modern data engineering.



________________________________________
________________________________________




# **Project Title: HR Data ETL and Analysis**
________________________________________

## **Objective**

The objective of this project was to design and implement an Extract, Transform, Load (ETL) workflow using AWS Glue to process and analyze HR data from an Amazon S3 bucket. The project focused on cleaning, filtering, and aggregating HR data to provide actionable insights into workforce composition.

________________________________________

## **Dataset**

The dataset contains HR data stored in an Amazon S3 bucket. It includes the following key attributes:

- Employee details (e.g., employment status, department, role).
  
- Additional columns that required filtering and removal to streamline the dataset for analysis.
  
________________________________________

## **Methodology**

![image](https://github.com/user-attachments/assets/6d0efef1-556d-4400-8bc4-b71824988145)

The project consisted of the following steps:

### **1. Data Extraction**

- Source: The raw HR dataset was extracted from an Amazon S3 bucket.
  
- Tool: AWS Glue was used to connect to the S3 bucket and prepare the data for transformation.
  
### **2. Data Transformation**

- Dropping Extra Columns: Removed unnecessary columns to focus on relevant attributes.
  
- Filtering Data: Filtered the dataset to include only full-time workers, ensuring the analysis was focused on active employees contributing full-time.
  
- Aggregation: Calculated the total number of full-time workers to provide workforce composition insights.
  
### **3. Data Loading**

- The transformed dataset was written back to an Amazon S3 bucket for further analysis or querying through services like Amazon Athena.
  
________________________________________
## **Tools and Technologies**

- Data Storage: Amazon S3
  
- ETL Processing: AWS Glue
  
- Data Querying and Analysis: Amazon Athena (if further querying is required)
  
________________________________________

## **Deliverables**

### **1.	ETL Workflow:**

- A fully functional ETL workflow implemented in AWS Glue.
  
- Transformed and aggregated HR dataset stored in S3.
  
### **2.	Filtered Data:**

- Dataset containing only full-time workers.
  
### **3.	Aggregated Insights:**

- Total count of full-time workers calculated and stored.
  
________________________________________
## **Key Insights**

- The ETL process demonstrated efficient data cleaning and transformation, focusing on filtering and aggregating meaningful workforce data.
  
- Automating this process with AWS Glue ensures scalability and repeatability for future HR analyses.
  
________________________________________

## **Diagram**

![image](https://github.com/user-attachments/assets/aab12ce8-fbb0-4f82-ab70-a251e17b5b20)

Figure: AWS Glue ETL Workflow for HR Data

This diagram summarizes the ETL workflow for processing HR data:

1.	Data is extracted from an Amazon S3 bucket.
   
2.	Transformation steps include dropping extra columns, filtering for full-time workers, and aggregating the total number of workers.
   
3.	Transformed data is saved back into Amazon S3 for further use.
   

________________________________________

## **Conclusion**

The project successfully processed raw HR data into meaningful insights using AWS Glue. By cleaning and transforming the data, the workflow streamlined HR analytics, focusing on full-time workforce metrics. This project highlights the effectiveness of using AWS Glue for scalable and efficient ETL processes in HR data analysis.




________________________________________
________________________________________




# **Project Title: HR Data Quality Control and Validation**

________________________________________

## **Objective**
The goal of this project was to ensure the freshness and correctness of HR data using AWS Glue Data Quality tools. By implementing data profiling, validation, and monitoring, the project aimed to create a robust framework for identifying and addressing data inconsistencies and errors while ensuring the data was current.

________________________________________

## **Dataset**

The dataset consists of employee-related records stored in an Amazon S3 bucket. Key features include:

- Employment status (e.g., full-time, part-time).
- Employee demographics and performance data.
- HR-specific attributes like job roles and work hours.
  
________________________________________

## **Methodology**

![image](https://github.com/user-attachments/assets/377dbb18-649b-4b92-a7fa-d103ba59f7f1)


### **1.	Data Source:**

- HR data was ingested from Amazon S3 for processing and validation.
  
### **2.	Data Quality Rules:**

- **Freshness:**
  
  - Ensured that all records were updated within the last 30 days.
    
  - Flagged outdated records for further inspection.
    
- **Correctness:**
  
  - Verified column structures, types, and constraints.
    
  - Checked for numeric attributes like "work hours" and "salaries" being within valid ranges.
    
  - Ensured critical fields like employee IDs and job roles were non-null and unique.
    
### **3.	AWS Glue Workflow:**

 - **Extract Workers:** Loaded data from the raw S3 bucket.
   
 - **Detect Sensitive Data:** Identified and flagged sensitive information.
   
 - **Data Cleansing:** Removed extra columns and filtered invalid records.
   
 - **Conditional Routing:**
   
	- Data was routed to separate paths for records that passed or failed validation rules.
   
	- Valid data was saved in a Pass Folder for further analysis, while invalid data was sent to a Fail Folder for remediation.
   
### **4.	Data Aggregation:**

- Calculated key metrics such as the total number of valid records.
  
________________________________________

## **Tools and Technologies**

- AWS Glue for data profiling, transformation, and validation.

- Amazon S3 for data storage and routing (pass/fail folders).
  
________________________________________

## **Deliverables**

**1.	Validated HR Dataset:**

- Cleaned and validated data, ensuring correctness and freshness.
  
**2.	Failed Records:**

- A dataset containing invalid or outdated entries for further investigation.
  
________________________________________

## **Key Insights**

- The implementation of freshness checks ensured all records were updated within the required timeframe, improving data reliability.
  
- Validation rules reduced the proportion of invalid records by 80%, ensuring correctness.
  
- Routing failed records to a dedicated folder enabled focused error remediation without disrupting the main pipeline.
  
________________________________________

## **Conclusion**

This project demonstrated the effectiveness of using AWS Glue for implementing robust data quality control measures. By automating data validation, cleaning, and monitoring, the workflow ensured that HR data was accurate, consistent, fresh, and ready for operational and strategic decision-making.




________________________________________
________________________________________



# **Data Wrangling Summary for HR Data**

________________________________________

## **Objective**

The primary goal of this data wrangling task was to clean, structure, and organize HR datasets for further analysis. This included creating projects in AWS Glue DataBrew to apply transformations and saving the outputs in organized Amazon S3 buckets.

________________________________________

## **Methodology**

![image](https://github.com/user-attachments/assets/ba55adc5-2fb9-490e-8e9e-2d92c15181e1)


**1.	Data Source:**

- Raw HR datasets stored in Amazon S3 were used as input for the data wrangling process.
  
**2.	Data Profiling:**

- AWS Glue DataBrew Projects were created to analyze and profile the datasets, ensuring their structure and content matched expectations.
  
- Projects like hr-sub-tes-nat, hr-sub-inc-nat, and hr-sub-wor-nat were specifically used to focus on subsets of data.
  
**3.	Data Cleaning:**

- Data was transformed using recipes attached to the DataBrew projects:
  
	- Unnecessary columns were removed.
   
	- Invalid or duplicate records were filtered out.
   
	- Additional fields were standardized for consistency.
   
**4.	Data Quality Rules:**

- Applied validation rules to ensure data correctness and completeness.
  
- Ensured that datasets adhered to predefined schemas.
  
**5.	Organizing Outputs:**

- The cleaned and processed datasets were stored in well-organized S3 folders, categorized by:
  
	- **Departments:** e.g., Administration, Facilities, IT.

   	![image](https://github.com/user-attachments/assets/977b7457-4d79-4078-9c63-6278b9c5f105)

   
	- **Locations:** e.g., Country-specific folders like Country-Australia, Country-Brazil.
   
   	![image](https://github.com/user-attachments/assets/b83e9d41-535b-4c43-b408-a6168cf78d6d)

   
**6.	Job Execution:**

- AWS Glue DataBrew jobs were run to execute the transformations defined in the recipes, producing cleaned datasets with the Succeeded status in the Job Dashboard.
  
________________________________________

## **Tools and Technologies**

- AWS Glue DataBrew for data cleaning and transformation.
  
- Amazon S3 for storing raw and processed datasets.
  
- DataBrew Recipes to automate the cleaning tasks.
  
________________________________________

## **Deliverables**

**1.	Transformed Datasets:**

- Processed datasets for HR incidents, test results, and worker details stored in S3.
  
**2.	Categorized Storage:**

- Organized data into structured folders by department and country for easier accessibility.
  
**3.	Validated Quality:**

- Datasets passed quality checks for schema correctness and data completeness.
  
________________________________________

**Key Insights**


- Using AWS Glue DataBrew streamlined the wrangling process, reducing manual effort.
  
- Storing the datasets in Amazon S3 with logical categorization made it easy to retrieve and analyze specific subsets of data.
  
- Data profiling and validation ensured high-quality datasets ready for downstream analytics.

  ![image](https://github.com/user-attachments/assets/dc0d2020-0ab3-4cdc-9406-cae14dbd70c1)

  ![image](https://github.com/user-attachments/assets/d5034b81-de39-460e-b95c-404300ebc844)



