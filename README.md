# **Project: Design and Implementation of a Data Analytics Platform for Vancouver**
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

The project consisted of the following phases:

### **1. Data Ingestion**

-	Stored the raw dataset in an Amazon S3 bucket (va-raw-nat), organized by ingestion year (2024).

-	Configured lifecycle rules to transition older data to Amazon S3 Glacier for cost-effective long-term storage.

### **2. Data Profiling**

-	Conducted profiling using AWS Glue DataBrew to analyze dataset characteristics.

-	Identified:

	 -	Missing values in critical fields (e.g., DATE_PLANTED, DIAMETER).

	 -	Outliers in numerical data.

	 -	Column correlations for potential enrichments.

### **3. Data Cleaning**

-	Addressed missing values and inconsistencies using AWS Glue transformations.

-	Performed:

	-	Standardization of column names and formats.

	-	Removal of invalid or duplicate records.

-	Stored the cleaned dataset in the va-trf-nat S3 bucket.

### **4. Data Enriching**

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

-	Established a governance framework to ensure data quality and compliance:

	-	Completeness: Ensured all critical fields (e.g., DATE_PLANTED, DIAMETER) were non-null.

	-	Freshness: Monitored datasets to ensure updates within a 30-day window.

	-	Validation Rules: Routed valid data to a "Pass Data" folder and invalid records to a "Failed Data" folder for remediation.

	-	Standardization: Applied transformations to align data types with the schema in the Glue Data Catalog.

### **7. Data Observability**

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

