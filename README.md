#### ** Analytical Database (Using Snowflake Schema)**

The analytical database will use a Snowflake Schema, which is highly normalized and ideal for complex queries used in reporting and analysis.

**Fact Tables:**

**a. Fact_Admissions**
   - **Admission_Fact_ID** (PK)
   - **Patient_ID** (FK)
   - **Ward_ID** (FK)
   - **Admission_DateTime**

**b. Fact_Tests**
   - **Test_Fact_ID** (PK)
   - **Patient_ID** (FK)
   - **Test_Type_ID** (FK)
   - **Result_ID** (FK)
   - **Test_DateTime**

**c. Fact_Prescriptions**
   - **Prescription_Fact_ID** (PK)
   - **Patient_ID** (FK)
   - **Medication_ID** (FK)
   - **Dosage**
   - **Start_Date**
   - **End_Date**

**Dimension Tables:**

**a. Dim_Patient**
   - **Patient_ID** (PK)
   - **Name**
   - **Date_of_Birth**
   - **Phone_Number_ID** (FK)
   - **Address_ID** (FK)

**b. Dim_Ward**
   - **Ward_ID** (PK)
   - **Name**
   - **Location**

**c. Dim_TestType**
   - **Test_Type_ID** (PK)
   - **Category**
   - **Description**

**d. Dim_Medication**
   - **Medication_ID** (PK)
   - **Medication**
   - **Type**

**e. Dim_Result**
   - **Result_ID** (PK)
   - **Result**
   - **Result_Description**

#### **Combining the Two for a Hybrid Model**

In the hybrid model:
- **Operational tasks** (like admissions, appointments) are managed using the ER diagram to ensure efficient, transactional data handling.
- **Analytical tasks** (like patient treatment outcomes, ward efficiency) are managed using the Snowflake schema to support detailed, complex queries that help in strategic decision-making.

#### **Integration Strategy**
- **Data Flow**: Data from the operational system (ER) flows into the analytical system (Snowflake) periodically through ETL (Extract, Transform, Load) processes.
- **Updates**: The analytical system is updated regularly (e.g., nightly) to reflect changes in the operational system, ensuring that reports and analyses reflect the most current data.

### **Conclusion**
This hybrid approach leverages the ER model for day-to-day hospital operations and the Snowflake model for in-depth data analysis, giving the National Hospital the flexibility to meet both immediate operational needs and strategic analytical requirements. This design ensures that the hospital can manage patient care efficiently while also gaining valuable insights from their
