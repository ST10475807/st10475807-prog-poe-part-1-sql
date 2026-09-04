# st10475807-prog-poe-part-1-sql
# RaceDayDB – Race Event Management Database

## 1. Project Overview

**RaceDayDB** is a relational database system designed to manage race events, organizers, participants, race categories, enrolments, and race results.

The database provides a structured way to store and manage information about race events and the people participating in them. It also demonstrates relationships between different entities using primary keys, foreign keys, constraints, and a bridge table for the many-to-many relationship between events and categories.

---

## 2. Project Objectives

The main objectives of the RaceDayDB project are to:

* Store organizer and participant information.
* Manage race events.
* Store different race categories and distances.
* Allow events to have multiple race categories.
* Allow participants to enrol in specific event categories.
* Store race results for participants.
* Maintain data integrity using database constraints.
* Demonstrate relationships between database tables.
* Provide queries for testing and verifying the database.

---

## 3. Database Name

```text
RaceDayDB
```

The database is designed for **Microsoft SQL Server** and can be executed using **SQL Server Management Studio (SSMS)**.

---

## 4. Database Structure

The database contains the following six main tables:

### Users

The `Users` table stores information about both organizers and participants.

Main fields include:

* `UserId`
* `FirstName`
* `LastName`
* `Email`
* `PasswordHash`
* `Role`
* `Phone`
* `CreatedAt`

The system restricts users to two roles:

```text
Organizer
Participant
```

---

### Events

The `Events` table stores information about races organized by users.

Main fields include:

* `EventId`
* `OrganizerId`
* `EventName`
* `Description`
* `EventDate`
* `Location`
* `Status`
* `CreatedAt`

Each event is associated with an organizer through the `OrganizerId` foreign key.

Event statuses include:

```text
Draft
Open
Closed
Completed
```

---

### Categories

The `Categories` table stores reusable race categories.

Examples included in the database are:

* 5K Fun Run
* 10K Road Race
* Half Marathon
* Trail Run

Each category can also contain a race distance in kilometres.

---

### EventCategories

`EventCategories` is the bridge table between `Events` and `Categories`.

It resolves the many-to-many relationship where:

* One event can contain multiple categories.
* One category can be used by multiple events.

The table also stores:

* Maximum participants
* Entry fee

The primary key consists of:

```text
EventId + CategoryId
```

---

### Enrolments

The `Enrolments` table records participants who register for event categories.

It stores:

* `EnrolmentId`
* `EventId`
* `CategoryId`
* `ParticipantId`
* `EnrolmentDate`
* `Status`

Enrolment statuses include:

```text
Active
Cancelled
Completed
```

The database also prevents the same participant from registering more than once for the same event category.

---

### Results

The `Results` table stores the results achieved by participants.

It contains:

* `ResultId`
* `EnrolmentId`
* `FinishPosition`
* `FinishTime`
* `ResultStatus`
* `RecordedAt`

Result statuses include:

```text
Pending
Finished
DNF
DNS
```

---

## 5. Relationships

The main relationships in the database are:

```text
Users
  |
  | 1:M
  |
Events
  |
  | M:N
  |
EventCategories
  |
  | M:1
  |
Categories

Users
  |
  | 1:M
  |
Enrolments
  |
  | 1:1
  |
Results
```

More specifically:

* One organizer can organize multiple events.
* One event belongs to one organizer.
* One event can have multiple categories.
* One category can belong to multiple events.
* One participant can have multiple enrolments.
* Each enrolment belongs to one participant.
* An enrolment can have one result.

---

## 6. Data Integrity

The database uses several SQL Server constraints to maintain data integrity.

### Primary Keys

Every major entity has a primary key.

Examples:

```text
Users.UserId
Events.EventId
Categories.CategoryId
Enrolments.EnrolmentId
Results.ResultId
```

The `EventCategories` table uses a composite primary key:

```text
(EventId, CategoryId)
```

### Foreign Keys

Foreign keys are used to maintain relationships between tables.

Examples include:

```text
Events.OrganizerId → Users.UserId

EventCategories.EventId → Events.EventId

EventCategories.CategoryId → Categories.CategoryId

Enrolments.ParticipantId → Users.UserId

Results.EnrolmentId → Enrolments.EnrolmentId
```

### Validation Constraints

The database also uses `CHECK`, `UNIQUE`, and `DEFAULT` constraints to prevent invalid data.

Examples include:

* Valid user roles.
* Valid event statuses.
* Valid enrolment statuses.
* Valid result statuses.
* Positive race distances.
* Positive maximum participant limits.
* Non-negative entry fees.
* Unique user email addresses.
* Unique participant/event/category enrolments.

---

## 7. Sample Data

The database includes sample data for demonstration and testing.

### Organizers

Two sample organizers are included.

### Participants

Two sample participants are included.

### Race Categories

Four categories are included:

```text
5K Fun Run
10K Road Race
Half Marathon
Trail Run
```

### Events

Three sample events are included:

```text
Polokwane Spring Run
Louis Trichardt Mountain Challenge
Limpopo Community Race Day
```

### Enrolments and Results

Sample participant enrolments and a race result are also included to demonstrate how the database operates.

---

## 8. Verification Queries

The SQL script contains queries that can be used to display the contents of each table.

Examples:

```sql
SELECT * FROM Users;

SELECT * FROM Events;

SELECT * FROM Categories;

SELECT * FROM EventCategories;

SELECT * FROM Enrolments;

SELECT * FROM Results;
```

A joined verification report is also included to combine participant, event, category, enrolment, and result information into a single report.

---

## 9. Technologies Used

* **Database:** Microsoft SQL Server
* **Language:** T-SQL
* **Database Management Tool:** SQL Server Management Studio (SSMS)
* **Version Control:** Git
* **Repository Platform:** GitHub

---

## 10. How to Run the Project

### Step 1 – Install SQL Server

Install Microsoft SQL Server and SQL Server Management Studio if they are not already installed.

### Step 2 – Open the SQL Script

Open the RaceDay database SQL script in SQL Server Management Studio.

### Step 3 – Execute the Script

Run the SQL script.

The script will:

1. Create the `RaceDayDB` database.
2. Remove existing tables when necessary.
3. Create the required tables.
4. Create primary and foreign key relationships.
5. Add validation constraints.
6. Insert sample data.
7. Run verification queries.
8. Produce a joined verification report.

### Step 4 – Verify the Database

After execution, check that the following tables have been created:

```text
Users
Events
Categories
EventCategories
Enrolments
Results
```

Run the verification queries to confirm that the sample data has been inserted correctly.

---

## 11. GitHub Development History

The project was developed incrementally using meaningful Git commits.

Example commit history:

```text
Initialise RaceDay database project
Create RaceDayDB database
Add database reset and table cleanup logic
Create Users table with primary key
Add user roles and validation constraints
Create Events table
Add organizer foreign key relationship to Events
Add event status and default constraints
Create Categories table
Add category uniqueness and distance validation
Create EventCategories bridge table
Add event-category foreign key relationships
Add participant limits and entry fee constraints
Create Enrolments table
Add enrolment relationships and status validation
Prevent duplicate participant enrolments
Create Results table
Add result validation and enrolment relationship
Insert sample organizer users
Insert sample participant users
Insert race categories and distances
Insert sample RaceDay events
Assign categories and entry fees to events
Insert sample enrolments and race results
Add database verification and joined reporting queries
```

This development history demonstrates the progressive construction of the database rather than presenting the database as a single completed script.

---

## 12. Project Files

A typical repository structure can be:

```text
RaceDayDB/
│
├── README.md
│
└── section-c-code.sql
```

If additional project documents are required, they can also be added to the repository.

---

## 13. Conclusion

The RaceDayDB project provides a relational database solution for managing race events and participant information.

The system demonstrates important database concepts including:

* Relational database design
* Primary keys
* Foreign keys
* Composite keys
* Many-to-many relationships
* Bridge tables
* Data validation
* Unique constraints
* Default constraints
* Sample data insertion
* SQL queries
* Joined reports

The database can be expanded in the future with additional functionality such as payments, race timing, notifications, certificates, event registration limits, and more detailed reporting.
