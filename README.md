# Power BI JIRA Analysis


![image](https://github.com/Utkarsh11-git/PowerBI_JIRA/assets/92782014/7dacb0a2-5bf0-45dc-90e8-cd6662859bce)



### ❓ Introduction:
This dashboard analyzes details of JIRA tickets using various variables such as Issues Assigned, Issues Resolved, Type of Issue, Time taken to resolve, Tickets reported by, etc. The findings from this will help plan and resolve the issues and improve the overall response and performance.

### Objective:
The primary objective of creating a dashboard to track Jira Software tickets is to provide a centralized, visualized view of project or issue-related data to support informed decision-making, enhance team collaboration, and monitor the progress of projects. It ensures that teams have the necessary insights to deliver projects successfully.

### Dataset Description:
* **Ticket No**: The number of the ticket assigned.
* **Assigned On**: The date on which the ticket was assigned by a user.
* **Resolved On**: The date of resolution.
* **Time Taken**: The number of days taken to resolve an issue.
* **Short Name**: The short name of the ticket to determine its issue type.
* **Type of Issue**: If the issue is a story, defect, Sub-Task, etc.
* **Reported By**: The person who reported the ticket.
* **Month Resoltion**: The month in which the ticket was resolved.
* **Month Assigned**: The month in which the ticket was assigned.

### 💡 DAX Formulas Used in Measures
**1. Total number of days taken to resolve a ticket excluding weekends**
* ``
Time-Taken = 
VAR StartDate = 'PowerBI-JIRA'[Assigned On]
VAR EndDate = 'PowerBI-JIRA'[Resolved On]
VAR NumWeekdays = 
    IF(
        StartDate = EndDate,  -- Check if the dates are the same
        0,  -- Return 0 if the dates are the same
        COUNTROWS(
            FILTER(
                CALENDAR(StartDate, EndDate),
                WEEKDAY([Date], 1) < 6
            )
        )
    )
RETURN
    NumWeekdays
``


**2. Issue Type of Ticket**
* `SWITCH('PowerBI-JIRA'[Short-Name],"ACM","Story","NGX","Defect","AAWIN","Sub-Task","RSAR","Defect","AAFWEH","Story","AM","Defect","AAADFS","Task","AAIIS","Task","MA","Sub-Task","AAFM","Epic","AMBA","Defect")`

### Insights:
* The majority of the issues were resolved within 10 days.
* Most of the tickets were created by Shimagami.
* The majority of the issues are defects, followed by Story.
* Nearly 60% of the tickets were assigned in the first 3 months of the cycle.
* Resolution of defects takes longer than the rest.
