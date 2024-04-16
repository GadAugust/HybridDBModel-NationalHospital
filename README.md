
### **ER schema for the operational database supporting daily transactions.**  

## Entities and Data Types           

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


## Conceptual Data Model Overview

To understand the structures and relationships defined within the National Hospital model, refer to the [View the Conceptual Data Model Documentation](https://github.com/GadAugust/HybridDBModel-NationalHospital/blob/The-conceptual-data-model/README.md). This documentation provides insights into the conceptual framework and the logical structure that underpins the database design.








