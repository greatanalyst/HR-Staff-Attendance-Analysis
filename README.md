# HR-Staff-Attendance-Analysis : Building An Interactive Power BI Dashboard For Staff Attendance 
## Table Of Content
- [Description](#description) 
- [Business Introduction](#business-introduction)
- [Business Problem](#business-problem)
- [Aim of the Project](#aim-of-the-project)
- [Solution](#solution)
- [Metrics Defined](#metrics-defined)
- [Features](#features)
- [Insights And Recommendations](#insights-and-recommendations)


### Description 

This project features an interactive HR Analytics Dashboard designed to track and analyze employee attendance patterns over a three-month period (April 2022 – June 2022). The goal of this dashboard is to provide HR managers with actionable insights into workforce presence, remote work trends, and sick leave patterns to improve operational efficiency.

<img width="1183" height="663" alt="image" src="https://github.com/user-attachments/assets/a6c9eb52-ae63-4a03-a17c-174e72af1d95" />

### Business Introduction

In the modern corporate landscape, human capital is an organization's most valuable asset. Managing a workforce effectively requires more than just tracking clock-ins; it requires a deep understanding of attendance patterns, remote work flexibility, and employee wellness.
This project introduces an HR Attendance Analytics solution designed for data-driven HR departments. The dashboard serves as a centralized hub to monitor employee engagement levels across multiple dimensions, providing a macro view of organizational health while allowing for micro-drills into individual performance and attendance reliability.

### Business Problem
- Manually tracking attendance through spreadsheets often leads to "data silos" where trends remain hidden. The organization faced several key challenges that this project aims to solve:

- Lack of Visibility into Hybrid Work Trends: With a growing Work-From-Home (WFH) culture, the management lacked clear data on how many employees were remote on specific days, making office space and resource planning difficult.

- Unidentified Attendance Dips: Without visual trend lines, the HR team could not easily identify specific periods (like the sharp drop to 77.92% in May) where attendance plummeted, preventing them from investigating root causes such as seasonal illness or morale issues.

- Inefficient Sick Leave Monitoring: Identifying "at-risk" employees who frequently take sick leave was a manual, time-consuming process. The business needed a way to instantly flag high SL Count % to provide proactive support or performance reviews.

- Inconsistent Weekly Coverage: Management needed to know if certain days of the week (e.g., Fridays) suffered from lower presence, which could impact client deliverables and team collaboration.

### Aim of the Project
The primary objective of this analysis is to transform raw attendance logs into a strategic asset for HR decision-making. Specifically, the analysis aims to:

- Optimize Hybrid Work Models: Determine the impact of Work From Home policies on overall productivity and office occupancy.

- Enhance Workforce Reliability: Identify patterns of absenteeism or frequent sick leave (SL) to trigger proactive wellness interventions.

- Data-Driven Scheduling: Analyze attendance by day of the week to ensure adequate staffing levels for client-facing operations.

- Individual Performance Tracking: Provide managers with a transparent, data-backed view of employee presence for quarterly reviews.
  
### Solution
This project followed a standard Data Analysis Expression (DAX) and ETL (Extract, Transform, Load) workflow.

Step 1: Data Connection & Cleaning Tool: Power Query (Power BI)
- Source Connection: Imported raw attendance data (CSV/Excel) containing daily status codes (P = Present, WFH = Work From Home, SL = Sick Leave).

- Unpivoting Columns: Since attendance data is often recorded with dates as headers, I unpivoted the date columns to create a "Long Format" table suitable for analysis.

- Data Typing: Ensured dates were recognized as Date types and status codes as Text.##### Key Features

Step 2: Data Modeling
- Calendar Table: Created a dedicated Date Table to allow for time-intelligence functions (filtering by Month, Weekday, and Date).

- Relationships: Established a One-to-Many relationship between the Employee Master list and the Attendance Fact table.

Step 3: DAX Measure Development

 I authored several custom measures to calculate the KPIs seen on the dashboard:

- Total working Days:           
  Total_working_days = 
  Var totaldays = COUNT('Final Data'[Value])
  VAR nonworkingdays = CALCULATE(COUNT('Final Data'[Value]), 'Final Data'[Value] IN {"WO", "HO"})
  RETURN
  totaldays-nonworkingdays

- Presnt Day:
  [Present Day ] = 
  VAR Presentday = CALCULATE(COUNT('Final Data'[Value]), 'Final Data'[Value] = "p")
  RETURN
  Presentday + [WFH COUNT M]

- Presence %:

  Presence % = DIVIDE([Present Day ],[Total_working_days])

- Work From Home Count:
  
  WFH COUNT M = SUM('Final Data'[WFH COUNT])

- Work From Home Count%:
  
  WFH COUNT % = DIVIDE([WFH COUNT M],[Present Day ], 0)

- Sick Leave Count:
  
  SL COUNT M = SUM('Final Data'[SL COUNT])

- Sick Leave Count %:
  
  SL COUNT % = DIVIDE([SL COUNT M],[Present Day ], 0)

Step 4: Visual Design & Interactivity
- KPI Cards: Placed at the top for an immediate "at-a-glance" health check of the company.

- Trend Analysis: Used Area Charts with trend lines to highlight volatility in attendance over the 3-month period.

- Matrix Reporting: Created a drill-down table for individual employee tracking.

- Slicers: Integrated "Month" slicers (Apr, May, Jun) to allow users to filter the entire dashboard by specific timeframes.

### Metrics Defined
- Presence %: The ratio of days an employee was physically or virtually present against total working days.

- WFH Count %: The percentage of days an employee worked from home.

- SL Count %: The frequency of sick leaves taken relative to the total period.

### Features
- Presence Tracking: Real-time monitoring of the overall presence percentage (currently at 91.83%).

- Work From Home (WFH) Analysis: Tracking the percentage of staff working remotely to balance office resources.

- Sick Leave (SL) Monitoring: Identifying trends in sick leave to manage wellness and backup staffing.

- Temporal Trends: Area charts showing daily fluctuations, allowing for the identification of specific dates with attendance drops (e.g., significant dips in May 2022).

- Granular Employee Data: A detailed table view breaking down attendance metrics by individual employee names.

- Day-of-the-Week Insights: Summarized tables showing which days of the week have the highest presence or remote work frequency.

###  Insights And Recommendations
1. Investigate the "May Slump"
The data shows a significant dip in Presence % during May 2022, reaching lows of 77.92%.
- Action: HR should cross-reference these dates with external factors such as local public holidays, seasonal flu outbreaks, or internal company events to determine if this was an anomaly or a recurring seasonal trend.
2. Formalize the "Friday-Monday" Hybrid Policy
The "WFH % by Day" table shows that Fridays (13.01%) and Thursdays (11.51%) have the highest remote work rates, while Tuesdays and Wednesdays are lower.
- Action: If the company requires high in-person collaboration, management should designate "Anchor Days" (e.g., Tuesday/Wednesday) where all staff are expected in-office, while maintaining the current flexibility for Mondays and Fridays to support work-life balance.
3. Proactive Wellness Interventions
Individual tracking reveals high SL Count % for specific employees (e.g., Ayanna Atkins at 0.18%, significantly higher than the 0.01% average).
- Action: Managers should conduct "Stay Interviews" or wellness check-ins with employees showing high sick leave frequency. This ensures they are supported and helps prevent long-term burnout or absenteeism.
4. Recognition for High Reliability
Employees like Alexander Davenport and Alyson Huber maintain 100% Presence.
- Action: Implement a "Reliability Award" or recognition program for top-tier attendance to reinforce a culture of consistency and dedication.


