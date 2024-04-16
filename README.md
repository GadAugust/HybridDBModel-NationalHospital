# HybridDBModel-NationalHospital
This GitHub repo hosts the data models and docs for a hybrid database model tailored for National Hospital, blending an ER Diagram for operational tasks and a Snowflake Schema for analytics. This setup optimizes daily hospital management and supports strategic data analysis, enhancing efficiency and decision-making capabilities.

### ***Objective Statement:***

The primary goal of this project is to design and implement a dual-purpose data management system for National Hospital. This innovative system will combine an Entity-Relationship (ER) diagram for managing daily operations with a Snowflake Schema for advanced data analytics. Our objective is to centralize the capture, storage, and retrieval of comprehensive healthcare data, simplifying processes and enhancing efficiency across the hospital's operations. This hybrid approach will not only streamline operational tasks but also bolster the hospital's capabilities in strategic decision-making through improved data analysis. By integrating these two powerful database models, National Hospital will enhance patient care quality and adapt more quickly to changing healthcare needs.

For an effective ER diagram for a National Hospital, it is essential to define not only the entities and relationships but also the appropriate data types for each attribute. This ensures that the database is optimized for performance and accuracy. Here’s a detailed schema of entities along with their attributes, primary keys, and proposed data types:

### **ER diagram for the operational database supporting daily transactions.**  

### **Entities and Data Types           

1. **Ward**
   - `Ward_ID` (PK): `INT`
   - `Name`: `VARCHAR(255)`
   - `Location`: `VARCHAR(255)`
   - `Capacity`: `INT`

2. **Patient**
   - `MRN` (PK): `INT`
   - `Name`: `VARCHAR(255)`
   - `Date_of_Birth`: `DATE`
   - `Phone_Numbers`: `VARCHAR(255)`  *(Multiple phone numbers can be stored as a delimited string or handled via a separate relationship table)*
   - `Address_City`: `VARCHAR(100)`
   - `Address_Street`: `VARCHAR(100)`
   - `Address_Code`: `VARCHAR(10)`
   - `Admission_DateTime`: `DATETIME`

3. **Doctor**
   - `Doctor_ID` (PK): `INT`
   - `Name`: `VARCHAR(255)`
   - `Specialty` (FK): `INT`
   - `Ward_ID` (FK): `INT`
   - `Contact_Number`: `VARCHAR(15)`

4. **Test**
   - `Episode_No` (PK): `INT`
   - `Patient_MRN` (FK): `INT`
   - `Category`: `VARCHAR(100)`
   - `Result`: `VARCHAR(255)`
   - `Test_DateTime`: `DATETIME`

5. **Specialty**
   - `Specialty_ID` (PK): `INT`
   - `Specialty_Name`: `VARCHAR(100)`
   - `Description`: `TEXT`

6. **Appointment**
   - `Appointment_ID` (PK): `INT`
   - `Patient_MRN` (FK): `INT`
   - `Doctor_ID` (FK): `INT`
   - `Appointment_DateTime`: `DATETIME`
   - `Purpose`: `VARCHAR(255)`
   - `Status`: `VARCHAR(50)`

7. **Prescription**
   - `Prescription_ID` (PK): `INT`
   - `Patient_MRN` (FK): `INT`
   - `Doctor_ID` (FK): `INT`
   - `Medication`: `VARCHAR(100)`
   - `Dosage`: `VARCHAR(50)`
   - `Start_Date`: `DATE`
   - `End_Date`: `DATE`
   - `Instructions`: `TEXT`

8. **Staff**
   - `Staff_ID` (PK): `INT`
   - `Name`: `VARCHAR(255)`
   - `Position`: `VARCHAR(100)`
   - `Contact_Number`: `VARCHAR(15)`
   - `Ward_ID` (FK): `INT`

9. **Equipment**
   - `Equipment_ID` (PK): `INT`
   - `Ward_ID` (FK): `INT`
   - `Name`: `VARCHAR(255)`
   - `Type`: `VARCHAR(100)`
   - `Status`: `VARCHAR(50)`
   - `Maintenance_Schedule`: `DATETIME`

10. **Room**
    - `Room_ID` (PK): `INT`
    - `Ward_ID` (FK): `INT`
    - `Capacity`: `INT`
    - `Type`: `VARCHAR(50)` *(e.g., single, shared)*

11. **Billing**
    - `Bill_ID` (PK): `INT`
    - `Patient_MRN` (FK): `INT`
    - `Amount`: `DECIMAL(10, 2)`
    - `Date`: `DATE`
    - `Status`: `VARCHAR(50)` *(e.g., paid, pending)*

12. **Insurance**
    - `Insurance_ID` (PK): `INT`
    - `Patient_MRN` (FK): `INT`
    - `Provider`: `VARCHAR(255)`
    - `Policy_Number`: `VARCHAR(100)`
    - `Coverage_Details`: `TEXT`

13. **Emergency Contact**
    - `Contact_ID` (PK): `INT`
    - `Patient_MRN` (FK): `INT`
    - `Name`: `VARCHAR(255)`
    - `Relationship`: `VARCHAR(100)`
    - `Phone_Number`: `VARCHAR(15)`

Each data type specified aims to optimize the database’s storage efficiency and query performance, ensuring that the system can handle extensive data inputs and retrievals effectively. The chosen data types reflect the expected format of the data, such as using `VARCHAR` for strings, `INT` for integers, `DECIMAL` for financial amounts, and `DATETIME` for timestamps


Creating a conceptual data model involves outlining the entities, their key attributes, and the relationships between them without specifying data types or detailed schema implementations. This high-level overview is useful for understanding the overall structure and relationships within the database before moving on to more detailed design phases. 

Below is a description of a conceptual data model for the National Hospital case study, which you can use as a guide to create a diagram in Lucidchart or a similar tool:

### **Conceptual Data Model Description**

1. **Ward**
   - **Attributes**: Ward_ID, Name, Location, Capacity
   - **Primary Key**: Ward_ID
   - **Relationships**:
     - One-to-Many with Patient (A Ward can host multiple Patients)
     - One-to-Many with Staff (A Ward can have multiple Staff members)
     - One-to-Many with Equipment (A Ward can contain multiple pieces of Equipment)
     - One-to-Many with Room (A Ward consists of multiple Rooms)

2. **Patient**
   - **Attributes**: MRN, Name, Date_of_Birth, Phone_Numbers, Address_City, Address_Street, Address_Code, Admission_DateTime
   - **Primary Key**: MRN
   - **Relationships**:
     - Many-to-One with Ward (A Patient is hosted in one Ward)
     - Many-to-Many with Doctor (A Patient can be examined by multiple Doctors, and a Doctor can examine multiple Patients)
     - One-to-Many with Test (A Patient can undergo multiple Tests)
     - One-to-Many with Appointment (A Patient can have multiple Appointments)
     - One-to-Many with Prescription (A Patient can have multiple Prescriptions)
     - One-to-Many with Billing (A Patient can have multiple Bills)
     - One-to-Many with Insurance (A Patient can have one Insurance record)
     - One-to-Many with Emergency Contact (A Patient can have multiple Emergency Contacts)

3. **Doctor**
   - **Attributes**: Doctor_ID, Name, Specialty, Contact_Number
   - **Primary Key**: Doctor_ID
   - **Relationships**:
     - Many-to-One with Specialty (A Doctor has one Specialty)
     - Many-to-Many with Patient (referenced above)
     - One-to-Many with Appointment (A Doctor can have multiple Appointments)
     - One-to-Many with Prescription (A Doctor can issue multiple Prescriptions)

4. **Test**
   - **Attributes**: Episode_No, Category, Result, Test_DateTime
   - **Primary Key**: Episode_No
   - **Relationships**:
     - Many-to-One with Patient (A Test is associated with one Patient)

5. **Specialty**
   - **Attributes**: Specialty_ID, Specialty_Name, Description
   - **Primary Key**: Specialty_ID
   - **Relationships**:
     - One-to-Many with Doctor (A Specialty can encompass multiple Doctors)

6. **Appointment**
   - **Attributes**: Appointment_ID, Appointment_DateTime, Purpose, Status
   - **Primary Key**: Appointment_ID
   - **Relationships**:
     - Many-to-One with Patient (An Appointment is for one Patient)
     - Many-to-One with Doctor (An Appointment is with one Doctor)

7. **Prescription**
   - **Attributes**: Prescription_ID, Medication, Dosage, Start_Date, End_Date, Instructions
   - **Primary Key**: Prescription_ID
   - **Relationships**:
     - Many-to-One with Patient (A Prescription is for one Patient)
     - Many-to-One with Doctor (A Prescription is issued by one Doctor)

...and so on for the remaining entities such as Staff, Equipment, Room, Billing, Insurance, and Emergency Contact, following a similar structure of identifying attributes, primary keys, and specifying the relationships they have with other entities.

### **Creating the Diagram in Lucidchart:**

- **Step 1**: Start by creating entities as boxes and name them according to the list above (e.g., Ward, Patient, Doctor).
- **Step 2**: Add attributes listed for each entity inside its box. You can simplify by mentioning only the key attributes for a more uncluttered diagram.
- **Step 3**: Draw relationships between entities using lines. Label the lines with the relationship type (e.g., One-to-Many, Many-to-One, Many-to-Many).
- **Step 4**: Where applicable, indicate the multiplicity of the relationships (e.g., 1:N for One-to-Many) near the connecting lines.
- **Step 5**: Review and ensure all entities are connected as per the described relationships and that the primary keys are indicated.

This conceptual model serves as a blueprint for understanding how data is interconnected within the National Hospital’s database, aiding in the development of a detailed logical and physical database design.








### **Snowflake schema for the data warehouse where data from various operational databases is consolidated for analysis and reporting.** 
