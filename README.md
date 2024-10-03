# Data Management Coursework

## Project Overview
This project focuses on designing and implementing a *Hospital Management System* using an *Entity-Relationship Diagram (ERD)* and a *Relational Schema*. The project encompasses both the logical and physical design phases.

Tools used:
- *ERD & Relational Schema Design*: draw.io
- *Database Design & Implementation*: Microsoft SQL Server Management Studio (SSMS)

### Key Entities in the Hospital Management System:
- Department
- Doctor
- Patient
- Appointment
- Report
- Nurse
- Room
- Bill

## ER Diagram
- *Platform Used*: draw.io
- *Files*:
  - ER Diagram (draw.io file)
  - ER Diagram (PNG)
  
    ![ER Diagram](https://github.com/user-attachments/assets/1e44fc5c-3c6f-43b5-bba0-0425bfa87db5)

## Relational Schema
- *Platform Used*: draw.io
- *Files*:
  - Relational Schema (draw.io file)
  - Relational Schema (PNG)
    
     ![Relational Schema Final](https://github.com/user-attachments/assets/cb95127c-6418-4d5a-af3b-48f9e4d45cd0)

## Physical Design Implementation
The database for the Hospital Management System was implemented using *Microsoft SQL Server Management Studio (SSMS)*.

### Instructions to Install SSMS:
1. Visit the [official download page](https://aka.ms/ssmsfullsetup).
2. Download the SSMS setup file.
3. Run the installer and follow the prompts.
4. Once installed, launch SSMS and connect to your SQL Server.

## Database Creation and Table Queries

### Creating the Database
sql
--Creating a database
CREATE DATABASE DM_Course_Work;


### Creating Tables

```sql

--Creating tables
CREATE TABLE Department(
    Department_ID    NVARCHAR(50) PRIMARY KEY NOT NULL,
    Department_Name  VARCHAR(255),
    Dep_Location     VARCHAR(255)
);

CREATE TABLE Nurse(
    Nurse_ID      NVARCHAR(50) PRIMARY KEY NOT NULL,
    Full_Name     VARCHAR(200),
    NIC           NVARCHAR(15) NOT NULL,
    Mobile        NVARCHAR(15),
    License_No    NVARCHAR(50),
    Department_ID NVARCHAR(50),
    CONSTRAINT FK_NurseDepartment FOREIGN KEY (Department_ID)
    REFERENCES Department(Department_ID)
);

CREATE TABLE Doctor(
    Doctor_ID      NVARCHAR(50) PRIMARY KEY NOT NULL,
    Full_Name      VARCHAR(255),
    NIC            NVARCHAR(15) NOT NULL,
    Mobile         NVARCHAR(15),
    Doc_Email      NVARCHAR(255),
    Specialization VARCHAR(100),
    License_No     NVARCHAR(50),
    Department_ID  NVARCHAR(50),
    CONSTRAINT FK_DoctorDepartment FOREIGN KEY (Department_ID)
    REFERENCES Department(Department_ID)
);

CREATE TABLE Patient(
    Patient_ID    NVARCHAR(50) PRIMARY KEY NOT NULL,
    Full_Name     VARCHAR(200),
    NIC           NVARCHAR(15) NOT NULL,
    DOB           DATE,
    Address       NVARCHAR(255),
    Mobile        NVARCHAR(15)    
);

CREATE TABLE Report(
    Report_ID     NVARCHAR(50) PRIMARY KEY NOT NULL,
    Report_Type   NVARCHAR(50),
    Date          DATE,
    Description   NVARCHAR(255),

    Doctor_ID     NVARCHAR(50),
    CONSTRAINT FK_ReportDoctor FOREIGN KEY (Doctor_ID)
    REFERENCES Doctor(Doctor_ID),

    Patient_ID    NVARCHAR(50),
    CONSTRAINT FK_ReportPatient FOREIGN KEY (Patient_ID)
    REFERENCES Patient(Patient_ID)
);

CREATE TABLE Appointment(
    Appointment_ID NVARCHAR(50) PRIMARY KEY NOT NULL,
    Placed_Date    DATE,
    Given_Date     DATE,

    Doctor_ID      NVARCHAR(50),
    CONSTRAINT FK_AppointmentDoctor FOREIGN KEY (Doctor_ID)
    REFERENCES Doctor(Doctor_ID),

    Patient_ID     NVARCHAR(50),
    CONSTRAINT FK_AppointmentPatient FOREIGN KEY (Patient_ID)
    REFERENCES Patient(Patient_ID)
);

CREATE TABLE Bill(
    Bill_Number    NVARCHAR(50) PRIMARY KEY NOT NULL,
    Payment_Type   VARCHAR(50),
    Amount         DECIMAL(10, 2),
    Date           DATE,

    Patient_ID     NVARCHAR(50),
    CONSTRAINT FK_BillPatient FOREIGN KEY (Patient_ID)
    REFERENCES Patient(Patient_ID)
);

CREATE TABLE Room_Type(
    Type_Name         VARCHAR(50) PRIMARY KEY NOT NULL,
    Charge_for_a_day  DECIMAL(10, 2)
);

CREATE TABLE Room(
    Room_Number   NVARCHAR(50) PRIMARY KEY NOT NULL,
    Availability  BOOLEAN,

    Room_Type     NVARCHAR(50),
    CONSTRAINT FK_RoomType FOREIGN KEY (Room_Type)
    REFERENCES Room_Type(Type_Name)
);

CREATE TABLE Room_Management(
    Room_Number   NVARCHAR(50),
    CONSTRAINT FK_RoomManagement FOREIGN KEY (Room_Number)
    REFERENCES Room(Room_Number),

    Patient_ID    NVARCHAR(50),
    CONSTRAINT FK_BillPatient FOREIGN KEY (Patient_ID)
    REFERENCES Patient(Patient_ID)
);
```
##
