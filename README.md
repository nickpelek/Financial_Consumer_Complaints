
# Project overview
This data analysis project aims to provide insights into the consumer complaints on financial products and services for a bank of America from 2017 to 2023. By analyzing different aspects of the complaints data, we ‘re looking to **identify trends**, **make data-driven recommendations** and **gain a deeper understanding about the consumer complaints.**

Insights and recommendations will be provided by answering some key questions, such as:
- Do consumer complaints have any seasonal patterns?
- Which State has the most complaints?
- Which products present the most complaints(+ What are their most common issue)?
- How does the company typically resolve the complaints?

## Tools used
- MS Excel (*Data exploring - Formatting*)
- MySQL workbench (*Data Analysis*)
- Tableau Public (*Creating Reports*)

**You can see the interactive Tableau Public dashboard [here](https://public.tableau.com/app/profile/nickpelek/viz/Financialconsumercomplaintsproject/Dashboard1)**
## Data Structure
Consumer Complaints database structure consists of two tables: *issues* & *states*, with a total row count of **62516** records.
![transparent er](https://github.com/user-attachments/assets/f884ca79-368d-4c44-a45e-d0b44b71c86c)



## Data Analysis Process (*SQL Queries*)

 >In this section we'll break down the project questions with SQL queries to find some useful insights.


- Do consumer complaints have any seasonal patterns?

   ```
  SELECT MONTH(date_submitted) AS months, COUNT(*) AS complaints FROM states
  GROUP BY MONTH(date_submitted)
  ORDER BY months;
  ``` 
![query 1](https://github.com/user-attachments/assets/a4cf482b-9308-4076-af58-7cc25dba18c4)
#####  *1 = January, 2 = February, 3 = March, 4 = April , 5 = May, 6 = June, 7 = July, 8 = August, 9 = September , 10 = October, 11 = November, 12 = December*  
> Consumer complaints do have a seasonal pattern, as they start to **increase** from *March* to *July*, followed by subsequent **decrease** in *August*.

- Which State has the most complaints?

  ```
  SELECT state, COUNT(*) AS total_complaints FROM states
  GROUP BY state
  ORDER BY total_complaints DESC
  LIMIT 1;
  ```
  ![query 2](https://github.com/user-attachments/assets/fdafc747-fcb2-4bed-91cd-0bebb086262d)

> The State with the **most complaints** is *California (CA)* with **13,709** complaints.

- 1) Which products present the most complaints?

  ```
  SELECT product, COUNT(complaint_id) AS complaints FROM issues
  GROUP BY product
  ORDER BY complaints DESC;
  ```
  ![query 3](https://github.com/user-attachments/assets/925a5b6e-fad3-4481-89b5-0252049e01fc)
>The products with the **most complaints** are: <br> 1) *Checking or Savings account* <br>
                                                 2) *Credit card or prepaid card* <br>
                                                 3) *Credit reporting, credit repair services, or other personal consumer reports*
 						

- 2) What are their most common issue?
     
  ```
  SELECT issue , COUNT(issue) AS total_issues FROM issues
  GROUP BY issue
  ORDER BY total_issues DESC;
  ```
  ![query 4](https://github.com/user-attachments/assets/8098de56-0127-4ba6-ac4d-8cce96215f28)
> The most common issue of those products is about **Managing an account**, with *15,109* people dealing with this problem.

- How does the company typically resolve the complaints?
  ```
  WITH total_complaints AS(
	  SELECT company_response_to_consumer, COUNT(complaint_id) AS complaints FROM issues
	  GROUP BY  company_response_to_consumer)
  SELECT company_response_to_consumer, CONCAT(ROUND(complaints/(SELECT count(complaint_id) FROM issues)*100,2), "%") AS percentage_complaints
  FROM total_complaints;
  ```
  ![query 5](https://github.com/user-attachments/assets/c51b0c85-aa1a-45c9-bbdf-3fc0ad8d68d6)
> A significant majority (*65.65%*) of complaints are resolved through explanation.
## Project Summary

Consumer complaints to the bank exhibit a seasonal pattern. Complaints remain **relatively low** on winter months, and start to increase from March till July, where they hit their peak (*with **6,455** complaints occured on **July***). **California (CA)** recorded the **highest** number of complaints (*13,709*), primarily related to **checking or savings accounts** (*24,814*). While most complaints (*65.65%*) were resolved **through explanations** from the bank to the consumer. Products most common issue is about **Managing an account**, with *15,109* complaints (**You can see that by *hovering* over the numbers of the '*Products with the most complaints*'  at the interactive** [Dashboard](https://public.tableau.com/app/profile/nickpelek/viz/Financialconsumercomplaintsproject/Dashboard1).


![Financial Consumer complaints Dashboard](https://github.com/user-attachments/assets/1f20b6bd-ae2c-42a6-af8f-360367c12269)

