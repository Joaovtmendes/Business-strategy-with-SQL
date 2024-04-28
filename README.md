# Business strategy with SQL

## Introduction:

I was hired as a data analyst at an Edtech company, a sector focused on education technology, with the goal of driving growth through data-driven strategies. The company's focus on accelerating its growth by increasing the number of registered users highlights the importance of understanding customer acquisition dynamics in the educational technology market. In response to this, I conducted a detailed analysis of various aspects of customer acquisition to assess the current status of new user growth within the company. The dashboard I developed provided valuable insights for the business team to develop actionable plans aimed at increasing the number of registered users and driving the company's growth.

## Project's goal:

- To analyze various aspects of customer acquisition to assess the current status of new user growth within the company.
- To develop a dashboard to provide valuable insights for the business team to develop actionable plans aimed at increasing the number of registered users and driving the company's growth.

## Technologies Used:

  <a href="https://www.metabase.com/" target="_blank" rel="noreferrer"> <img src="https://github.com/Joaovtmendes/Business-strategy-with-SQL/assets/154254190/5b6a10d2-0590-456b-b77a-bc57becbab19" alt="Metabase" width="40" height="40" style="display:inline;"/> </a>
  <a href="https://www.microsoft.com/en-us/sql-server" target="_blank" rel="noreferrer"> <img src="https://www.svgrepo.com/show/303229/microsoft-sql-server-logo.svg" alt="mssql" width="40" height="40"/> </a> 
  <a href="https://www.microsoft.com/pt-br/microsoft-365/excel" target="_blank" rel="noreferrer"> <img src="https://seeklogo.com/images/E/excel-logo-974BFF9CB9-seeklogo.com.png" alt="excel" width="40" height="40"/> 

## Methodology:

Excel was used to perform the steps of understanding and preparing the spreadsheet data for the number of registered users:

- Checked for null values.
- Checked for duplicate rows.
- Reviewed the description and count of each column.
  
Subsequently, SQL Server was used to process and filter the data using the necessary queries for the analysis of registered users.

### Analyses conducted through the queries:

- **Distribution by gender:**
  SELECT
  `leads_basic_details`.`gender` AS `gender`,
  COUNT(*) AS `count`
FROM
  `leads_basic_details`
GROUP BY
  `leads_basic_details`.`gender`
ORDER BY
  `leads_basic_details`.`gender` ASC
  
- **Number of leads by education level:**
  SELECT
  `leads_basic_details`.`current_education` AS `current_education`,
  COUNT(*) AS `count`
FROM
  `leads_basic_details`
GROUP BY
  `leads_basic_details`.`current_education`
ORDER BY
  `count` ASC,
  `leads_basic_details`.`current_education` ASC
  
- **Average age:**
  SELECT
  AVG(`leads_basic_details`.`age`) AS `avg`
FROM
  `leads_basic_details`
  
- **Watched Media:**
  SELECT
  `leads_demo_watched_details`.`language` AS `language`,
  AVG(
    `leads_demo_watched_details`.`watched_percentage`
  ) AS `avg`
FROM
  `leads_demo_watched_details`
WHERE
  `leads_demo_watched_details`.`watched_percentage` > 0.5
GROUP BY
  `leads_demo_watched_details`.`language`
ORDER BY
  `leads_demo_watched_details`.`language` DESC
  
- **Number of calls answered by platform:**
  SELECT
  `leads_basic_details__via__lead_id`.`lead_gen_source` AS `leads_basic_details__via__lead_id__lead_gen_source`,
  `leads_interaction_details`.`call_done_date` AS `call_done_date`,
  COUNT(*) AS `count`
FROM
  `leads_interaction_details`
LEFT JOIN `leads_basic_details` AS `Leads Basic Details - Lead` ON `leads_interaction_details`.`lead_id` = `Leads Basic Details - Lead`.`lead_gen_source`
  LEFT JOIN `leads_basic_details` AS `leads_basic_details__via__lead_id` ON `leads_interaction_details`.`lead_id` = `leads_basic_details__via__lead_id`.`lead_id`
WHERE
  `leads_interaction_details`.`call_status` = 'successful'
GROUP BY
  `leads_basic_details__via__lead_id`.`lead_gen_source`,
  `leads_interaction_details`.`call_done_date`
ORDER BY
  `leads_basic_details__via__lead_id`.`lead_gen_source` ASC,
  `leads_interaction_details`.`call_done_date` ASC

## Results:

In the data visualization process, Metabase was used to create dashboards and graphs using SQL queries. Through these analyses, it was possible to identify that:

- **Gender Distribution:** The population consists of 55% females and 45% males, indicating a slightly higher representation of females.
- **Lead Sources:** The majority of leads come from people looking for a job or from B.tech, suggesting that these are the primary demographics or interests of the leads.
- **Average Age:** The average age of the population is 22 years old, indicating a relatively young demographic.
- **Language:** English is the most spoken language among the population, based on the media shows watched.
- **Lead Volume Trends:** There was a large volume of leads in January across different platforms, but in February, there was a general drop in leads, with some recovery towards the end of February. This trend suggests a seasonal or temporary change in lead generation patterns.

<p align="center">
<img  width="80%" src="https://github.com/Joaovtmendes/Business-strategy-with-SQL/assets/154254190/f1980ab5-fffa-4673-bb0d-33d3145c01e7">
</p>
