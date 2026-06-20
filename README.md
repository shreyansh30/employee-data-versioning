# Employee Data Versioning using Delta Lake

## Overview

This project demonstrates how Delta Lake can be used to maintain versioned employee records in Azure Databricks.

The solution simulates real-world employee lifecycle events such as salary revisions, department transfers, onboarding of new hires, and employee exits while preserving historical versions of data through Delta Lake transaction logs.

The project showcases Delta Lake features including:

- ACID Transactions
- UPDATE
- MERGE
- DELETE
- Version History
- Time Travel
- Auditability

---

## Technologies Used

- Azure Databricks
- Delta Lake
- Apache Spark (PySpark)
- SQL
- GitHub

---

## Dataset

Dataset Source:

IBM HR Analytics Employee Attrition Dataset

Dataset Statistics:

- Records: 1,470 Employees
- Attributes: 35 Columns
- Primary Key: EmployeeNumber

Key Business Columns Used:

- EmployeeNumber
- Department
- JobRole
- MonthlyIncome
- Attrition

---

## Architecture

```mermaid
flowchart TD
    A[Employee CSV Dataset] --> B[Azure Databricks]
    B --> C[Delta Lake Table]

    C --> D[Salary Updates]
    C --> E[Department Transfers]
    C --> F[New Hire MERGE]
    C --> G[Employee Exits DELETE]

    D --> H[Delta Transaction Log]
    E --> H
    F --> H
    G --> H

    H --> I[Version History]
    H --> J[Time Travel]
```

---

## Project Workflow

### Version 0 – Initial Load

The employee dataset was loaded into Azure Databricks and persisted as a Delta Lake table.

Result:

- Delta Table Created
- Version 0 Generated

---

### Version 1 – Salary Revision Cycle

A salary increase was applied to eligible employees using Delta UPDATE operations.

Features Demonstrated:

- UPDATE
- ACID Transactions

---

### Version 4 – Department Transfers

326 employee records were transferred between departments.

Features Demonstrated:

- UPDATE
- Version Tracking

---

### Version 6 – New Hire Processing

20 new employee records were generated programmatically using PySpark and merged into the Delta table.

Employee Count:

- Before MERGE: 1470
- After MERGE: 1490

Features Demonstrated:

- MERGE
- UPSERT Operations

---

### Version 8 – Employee Exits

Employees with Attrition = 'Yes' were removed from the employee table.

Rows Deleted:

- 237 Employees

Employee Count:

- Before DELETE: 1490
- After DELETE: 1253

Features Demonstrated:

- DELETE
- Delta Versioning

---

## Delta Lake Time Travel

Delta Lake allows querying historical versions of data.

Example:

```sql
SELECT *
FROM employee_db.employee_versioned
VERSION AS OF 6;
```

Results:

- Version 6 Employee Count: 1490
- Current Employee Count: 1253

Deleted records remain accessible through historical versions.

---

## Version History

The Delta transaction log maintains a complete audit trail of all operations.

Operations performed:

| Version | Operation |
|----------|-----------|
| 0 | Initial Load |
| 1 | UPDATE |
| 2 | OPTIMIZE |
| 3 | UPDATE |
| 4 | UPDATE |
| 5 | OPTIMIZE |
| 6 | MERGE |
| 7 | OPTIMIZE |
| 8 | DELETE |

---

## Screenshots

### Dataset Loaded

![Dataset Loaded](screenshots/01_dataset_loaded.png)

### Delta Table Created

![Delta Table](screenshots/02_delta_table_created.png)

### Complete Version History

![History](screenshots/03_complete_version_history.png)

### Salary Update

![Salary Update](screenshots/04_salary_update.png)

### Department Transfer

![Department Transfer](screenshots/05_department_transfer.png)

### MERGE New Hires

![MERGE](screenshots/06_merge_new_hires.png)

### Employee Delete

![Delete](screenshots/07_delete_employees.png)

### Time Travel

![Time Travel](screenshots/08_time_travel_recovery.png)

### Final Employee Table

![Final Table](screenshots/09_final_employee_table.png)

---

## Key Learnings

- Delta Lake transaction logs
- ACID-compliant data operations
- Delta UPDATE statements
- Delta MERGE operations
- Delta DELETE operations
- Time Travel and Version Recovery
- Historical Auditing
- Azure Databricks Development Workflow

---

## Author

Shreyansh Kumar

B.Tech Computer Science & Communication Engineering

KIIT University
