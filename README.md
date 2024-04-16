## **Analytical Database (Using Snowflake Schema)**

The analytical database will use a Snowflake Schema, which is highly normalized and ideal for complex queries used in reporting and analysis.
To effectively design a Snowflake Schema that complements the ERD for National Hospital's OLAP (Online Analytical Processing) needs, we will structure the database to optimize for query performance and support complex analytical queries. This design will focus on decomposing the ERD into a series of dimension and fact tables which will enable multidimensional analysis typical in a Snowflake Schema.

## **Snowflake Schema Design**

#### **Fact Tables**

1. **Fact_Admissions**
   - **Primary Key**: Admission_ID
   - **Foreign Keys**: Patient_ID, Ward_ID
   - **Measures**: Length_of_Stay (calculated as difference between Admission_DateTime and Discharge_DateTime, if available)
   - **Dimensions Linked**: Dim_Patient, Dim_Ward, Dim_Time

2. **Fact_Prescriptions**
   - **Primary Key**: Prescription_ID
   - **Foreign Keys**: Patient_ID, Doctor_ID, Medication_ID
   - **Measures**: Quantity_Prescribed (based on Dosage), Duration (calculated from Start_Date to End_Date)
   - **Dimensions Linked**: Dim_Patient, Dim_Doctor, Dim_Medication, Dim_Time

3. **Fact_Tests**
   - **Primary Key**: Test_ID
   - **Foreign Keys**: Patient_ID
   - **Measures**: Test_Result (quantifiable result if applicable)
   - **Dimensions Linked**: Dim_Patient, Dim_Test, Dim_Time

4. **Fact_Billing**
   - **Primary Key**: Bill_ID
   - **Foreign Keys**: Patient_ID
   - **Measures**: Amount_Billed, Amount_Paid, Outstanding_Amount (calculated as Amount_Billed - Amount_Paid)
   - **Dimensions Linked**: Dim_Patient, Dim_Time

#### **Dimension Tables**

1. **Dim_Patient**
   - **Primary Key**: Patient_ID
   - **Attributes**: Name, Date_of_Birth, Phone_Numbers, Address_City, Address_Street, Address_Code
   - **Role**: Patient demographics and other specifics for use in all fact tables where patient details are necessary.

2. **Dim_Doctor**
   - **Primary Key**: Doctor_ID
   - **Attributes**: Name, Specialty_ID, Contact_Number
   - **Role**: Doctor details useful for prescriptions and patient treatment analysis.

3. **Dim_Ward**
   - **Primary Key**: Ward_ID
   - **Attributes**: Name, Location, Capacity
   - **Role**: Details about hospital wards for admission analytics and resource usage.

4. **Dim_Medication**
   - **Primary Key**: Medication_ID (derived attribute from Prescription using Medication name as unique identifier)
   - **Attributes**: Medication, Type, Typical_Dosage
   - **Role**: Information on medications for analyzing prescription patterns.

5. **Dim_Test**
   - **Primary Key**: Test_ID (derived attribute from Test using Episode_No as unique identifier)
   - **Attributes**: Category, Normal_Range_Low, Normal_Range_High
   - **Role**: Specifics about tests conducted to facilitate detailed test result analysis.

6. **Dim_Time**
   - **Primary Key**: Date_Key
   - **Attributes**: Date, Day, Month, Quarter, Year
### **Role**: Time dimension for performing trend analysis over different time frames.

7. **Dim_Room**
   - **Primary Key**: Room_ID
   - **Attributes**: Ward_ID, Capacity, Type
   - **Role**: Details about rooms to analyze patient accommodation patterns and ward capacity utilization.

8. **Dim_Insurance**
   - **Primary Key**: Insurance_ID
   - **Attributes**: Provider, Policy_Number, Coverage_Details
   - **Role**: Insurance details for financial analysis and billing purposes.

#### **Schema Relationships**

- **Patient-Centric Analysis**: Central to understanding patient flow, treatment, and outcomes. Links across admissions, tests, and billing fact tables.
- **Resource Utilization**: Analyzing how effectively wards, rooms, and medications are used relative to patient care and hospital operations.
- **Financial Insights**: Billing and insurance data integrated to provide a comprehensive financial overview, crucial for cost management and revenue optimization.

#### **Usage and Implementation**

- This schema will facilitate complex analytical queries, enabling the hospital to extract detailed insights into patient demographics, treatment outcomes, resource utilization, and financial management.
- The design supports ad-hoc reporting and multidimensional analysis, which are essential for strategic planning and operational improvements in a hospital setting.
- Implementation would involve setting up ETL processes to regularly populate and update the OLAP database from the OLTP system, ensuring data freshness and reliability.




