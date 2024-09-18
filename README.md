# Financial Consumer Complaints

## Project overview
This data analysis project aims to provide insights into the consumer complaints on financial products and services for a bank of America from 2017 to 2023. By analyzing different aspects of the complaints data, we ‘re looking to **identify trends**, **make data-driven recommendations** and **gain a deeper understanding about the consumer complaints.**

## Exploratory Data Analysis (E.D.A.)
With the *E.D.A.* consumer complaints are explored to answer some key questions, such as:
- Do consumer complaints have any seasonal patterns?
- Which State has the most complaints?
- Which products present the most complaints(+ What are their most common issue)?
- How does the company typically resolve the complaints?

## Tools used
- MS Excel (*Data exploring - Formatting*)
- MySQL workbench (*Data Analysis*)
- Tableau Public (*Creating Reports*)

## Data Structure
Consumer Complaints database structure consists of two tables: *issues* & *states*, with a total row count of **62516** records.
![er diagram copy](https://github.com/user-attachments/assets/f4e2a1f5-41b7-46a8-a562-acaa795004c9)

## Data Analysis Process (*SQL Queries*)

 >In this section we'll break down the project questions with SQL queries to find some useful insights.


- Do consumer complaints have any seasonal patterns?

   ```
  SELECT MONTH(date_submitted) AS months, COUNT(*) AS complaints FROM states
  GROUP BY MONTH(date_submitted)
  ORDER BY months;
  ```
> Consumer complaints do have a seasonal pattern, as they start to **increase** from *March* to *July*, <br> followed by subsequent **decrease** in *August*.

- Which State has the most complaints?

  ```
  SELECT state, COUNT(*) AS total_complaints FROM states
  GROUP BY state
  ORDER BY total_complaints DESC
  LIMIT 1;
  ```
> The State with the **most complaints** is *California (CA)* with **13,709** complaints.

- 1) Which products present the most complaints?
     
  ```
  SELECT product, COUNT(complaint_id) AS complaints FROM issues
  GROUP BY product
  ORDER BY complaints DESC;
  ```
>The products with the **most complaints** are: <br> 1) *Checking or Savings account* <br>
                                                 2) *Credit card or prepaid card* <br>
                                                 3) *Credit reporting, credit repair services, or other personal consumer reports*
 						

- 2) What are their most common issue?
  ```
  SELECT issue , COUNT(issue) AS total_issues FROM issues
  GROUP BY issue
  ORDER BY total_issues DESC;
  ```
> The most common issue of those products is about **Managing an account**, with *15,109* people dealing with this problem.

- How does the company typically resolve the complaints?
  ```
  WITH total_complaints AS(
	  SELECT company_response_to_consumer, COUNT(complaint_id) AS complaints FROM issues
	  GROUP BY  company_response_to_consumer)
  SELECT company_response_to_consumer, CONCAT(ROUND(complaints/(SELECT count(complaint_id) FROM issues)*100,2), "%") AS percentage_complaints
  FROM total_complaints;
  ```
> A significant majority, 65.65%, of complaints are resolved through explanation.
### Results
The analysis results are summarized as follows:
- Consumer complaints show a clear seasonal trend, with a steady increase from March to July and then drecreasing steadily.
- The State with the most complaints(*13,709*) is California (*CA*)
- The products with the most complaints are:
    1) Checking or savings account (*24,814*)
    2) Credit card or prepaid card(*16,197*)
    3) Credit reporting, credit repair services, or other personal consumer reports (*7,710*)
- Products most common issue is managing an account(*with 15,109 complaints*)
- The company typically close complaints with an explanation (*with 65,65% of total*)
