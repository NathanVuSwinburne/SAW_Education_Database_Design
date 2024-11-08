# SAW Education Database Design

## Project Overview
This project presents a structured relational database design for **SAW Education**, a consultancy company specializing in study abroad and immigration services that I had a chance to work at. Developed in MySQL, this new database structure enhances data organization, streamlines operational processes, and provides actionable insights through structured queries. The design addresses previous inefficiencies, enabling better data integrity and facilitating strategic business decisions.

### Team Members
- **Thanh Nam Vu** - Student ID: 104991276
- **Tutorial Time**: Thursday, 4:30 PM
- **Swinburne University of Technology**

## Objectives
- **Enhance Data Integrity**: Ensure consistent data by implementing primary and foreign keys, enforcing referential integrity.
- **Optimize Operations**: Reduce data redundancy, improve retrieval times, and support streamlined workflows across departments.
- **Data-Driven Insights**: Enable business insights through SQL queries for event effectiveness, client conversion tracking, and case profitability.
- **Decision Support**: Provide managers with a foundation for evaluating event effectiveness, counselor workloads, and client progress.

## Database Design
### Key Entities and Relationships
The database is structured around seven main entities, each representing a core aspect of SAW Education’s business model:
1. **Event**: Stores details about lead-generating events.
2. **Attendee**: Tracks individuals attending events.
3. **Client**: Contains information on potential clients, linked to events.
4. **Appointment**: Records meetings between clients and counselors.
5. **Counselor**: Holds counselor details to manage workloads.
6. **Cases**: Represents enrolled clients and tracks profitability.
7. **University**: Stores information on universities clients apply to.

### Entity-Relationship Diagram (ERD)
The ERD defines relationships between these entities, supporting efficient data flow and minimal redundancy.

### Table Structure
Each table utilizes primary keys for unique identification and foreign keys to maintain referential integrity. Key relationships include:
- **Event - Attendee** (One-to-Many): Links events to attendees.
- **Attendee - Client** (One-to-One / One-to-Many): Links attendees who become clients.
- **Client - Appointment** (One-to-Many): Connects clients with multiple appointments.
- **Client - Cases** (One-to-One): Connects clients who commit to cases.
- **Cases - University** (Many-to-One): Allows multiple cases per university.

## SQL Queries for Business Insights
The following queries generate insights that support strategic decision-making:

1. **Most Effective Event**: Identifies events with the highest client conversions.
   ```sql
   SELECT e.EventName, COUNT(DISTINCT c.ClientID) AS ClientCount
   FROM Event e
   JOIN Attendee a ON e.EventID = a.EventID
   JOIN Client c ON a.AttendeeID = c.ClientID
   GROUP BY e.EventName
   ORDER BY ClientCount DESC;
   
2. **Client Conversions by Event**: Tracks clients from each event who become cases.
   ```sql
   SELECT e.EventName, COUNT(DISTINCT cs.CaseID) AS CaseCount
   FROM Event e
   JOIN Attendee a ON e.EventID = a.EventID
   JOIN Client c ON a.AttendeeID = c.ClientID
   JOIN Cases cs ON c.ClientID = cs.ClientID
   GROUP BY e.EventName
   ORDER BY CaseCount DESC;
3. **Counselor Workload**: Summarizes appointments handled by each counselor.
   ```sql
   SELECT co.CounselorName, COUNT(ap.AppointmentID) AS AppointmentCount
   FROM Counselor co
   JOIN Appointment ap ON co.CounselorID = ap.CounselorID
   GROUP BY co.CounselorName
   ORDER BY AppointmentCount DESC;
4. **Popular University Choices**: Identifies frequently chosen universities.
   ```sql
   SELECT u.UniversityName, COUNT(DISTINCT CaseID) AS CasesCount
   FROM University u
   JOIN Cases cs ON u.UniversityID = cs.UniversityID
   GROUP BY u.UniversityName
   ORDER BY CasesCount DESC;
5. **Profit by Event**: Shows total profit generated per event.
   ```sql
   SELECT e.EventName, SUM(cs.ProfitGenerated) AS TotalProfit
   FROM Event e
   JOIN Attendee a ON e.EventID = a.EventID
   JOIN Client c ON a.AttendeeID = c.ClientID
   JOIN Cases cs ON c.ClientID = cs.ClientID
   GROUP BY e.EventName;
## Technologies Used
- **Database**: MySQL
- **Data Structure**: Primary and foreign keys, normalization techniques, indexing

## Future Improvements
- **Advanced Analytics**: Develop additional queries to track client behavior trends and improve marketing strategies.
- **Visualization Integration**: Integrate with a BI tool (e.g., Tableau, Power BI) for data visualization and enhanced analytics.

## Summary
This database structure enhances SAW Education's data management by ensuring consistent data, reducing redundancy, and supporting strategic decisions. The design equips SAW Education to track client journeys from initial event attendance to enrollment, while also providing essential insights into event performance and case profitability, laying the foundation for future data-driven growth.

  
