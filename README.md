
##  This high-level overview is useful for understanding the overall structure and relationships within the database before moving on to more detailed design phases. 

This conceptual data model provides a comprehensive overview of the interrelations between the various entities within the National Hospital's database system. It captures all necessary details to facilitate efficient data management and accessibility for enhanced hospital operations and patient care. This model is primed for further development into a fully relational database schema, which will be crucial for the implementation phase of the database system.

### **Conceptual Data Model Description**

**1. Ward**
- **Attributes**: Ward_ID, Name, Location, Capacity
- **Primary Key**: Ward_ID
- **Relationships**:
  - One-to-Many with Patient (A Ward can host multiple Patients)
  - One-to-Many with Staff (A Ward can have multiple Staff members)
  - One-to-Many with Equipment (A Ward can contain multiple pieces of Equipment)
  - One-to-Many with Room (A Ward consists of multiple Rooms)

**2. Patient**
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

**3. Doctor**
- **Attributes**: Doctor_ID, Name, Specialty, Contact_Number
- **Primary Key**: Doctor_ID
- **Relationships**:
  - Many-to-One with Specialty (A Doctor has one Specialty)
  - Many-to-Many with Patient (referenced above)
  - One-to-Many with Appointment (A Doctor can have multiple Appointments)
  - One-to-Many with Prescription (A Doctor can issue multiple Prescriptions)

**4. Test**
- **Attributes**: Episode_No, Category, Result, Test_DateTime
- **Primary Key**: Episode_No
- **Relationships**:
  - Many-to-One with Patient (A Test is associated with one Patient)

**5. Specialty**
- **Attributes**: Specialty_ID, Specialty_Name, Description
- **Primary Key**: Specialty_ID
- **Relationships**:
  - One-to-Many with Doctor (A Specialty can encompass multiple Doctors)

**6. Appointment**
- **Attributes**: Appointment_ID, Appointment_DateTime, Purpose, Status
- **Primary Key**: Appointment_ID
- **Relationships**:
  - Many-to-One with Patient (An Appointment is for one Patient)
  - Many-to-One with Doctor (An Appointment is with one Doctor)

**7. Prescription**
- **Attributes**: Prescription_ID, Medication, Dosage, Start_Date, End_Date, Instructions
- **Primary Key**: Prescription_ID
- **Relationships**:
  - Many-to-One with Patient (A Prescription is for one Patient)
  - Many-to-One with Doctor (A Prescription is issued by one Doctor)

**8. Staff**
- **Attributes**: Staff_ID, Name, Position, Contact_Number
- **Primary Key**: Staff_ID
- **Relationships**:
  - Many-to-One with Ward (Staff are assigned to Wards)

**9. Equipment**
- **Attributes**: Equipment_ID, Name, Type, Status, Maintenance_Schedule
- **Primary Key**: Equipment_ID
- **Relationships**:
  - Many-to-One with Ward (Equipment is stored in Wards)

**10. Room**
- **Attributes**: Room_ID, Type, Capacity
- **Primary Key**: Room_ID
- **Relationships**:
  - Many-to-One with Ward (Rooms are part of Wards)

**11. Billing**
- **Attributes**: Bill_ID, Amount, Date, Status
- **Primary Key**: Bill_ID
- **Relationships**:
  - Many-to-One with Patient (Bills are issued to Patients)

**12. Insurance**
- **Attributes**: Insurance_ID, Provider, Policy_Number, Coverage_Details
- **Primary Key**: Insurance_ID
- **Relationships**:
  - Many-to-One with Patient (Patients are covered by Insurance)

**13. Emergency Contact**
- **Attributes**: Contact_ID, Name, Relationship, Phone_Number
- **Primary Key**: Contact_ID
- **Relationships**:
  - Many-to-One with Patient (Patients have Emergency Contacts)







