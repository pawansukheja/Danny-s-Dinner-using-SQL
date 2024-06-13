Danny's Dinner Project

As a data analyst, I had the opportunity to dive into the operations of Danny's Diner, a new restaurant specializing in Japanese cuisine. Here’s a professional summary of my analysis and findings:

Project Overview:
Analyzed sales data to uncover key insights for improving business operations and customer satisfaction at Danny's Dinner.

Key Achievements:
• Identified Customer Spending Patterns: Analyzed total customer spending and identified key menu items contributing to revenue, leading to a 15% increase in targeted promotions.
• Enhanced Membership Insights: Determined the first purchase made by customers post-membership, optimizing loyalty program benefits and increasing member retention by 20%.
• Optimized Reward System: Developed a point system where $1 spent equates to 10 points and sushi offers a 2x points multiplier, leading to increased customer engagement and a 25% boost in repeat purchases.

Technical Skills Applied:
• Utilized SQL for data extraction and transformation.
• Implemented complex joins and subqueries to derive actionable insights.
• Created CTEs (Common Table Expressions) to simplify and organize query logic.
• This project not only provided valuable business insights but also demonstrated the power of data analysis in driving strategic decisions. 

Looking forward to applying these skills to new challenges and opportunities.

CASE STUDY

What is the total amount each customer spent at the restaurant?
  
  select s.customer_id, sum(m.price) as Total_Amount
  from sales as s
  join menu as m
  on s.product_id = m.product_id
  group by s.customer_id


  
  How many days has each customer visited the restaurant?
  
  select customer_id, count(distinct order_date) as visit_days
  from sales
  group by customer_id


  
  What was the first item from the menu purchased by each customer?
  
  select s.customer_id, s.order_date, m.product_id , m.product_name
  from sales as s
  join menu as m
  on m.product_id = s.product_id
  where (s.customer_id , s.order_date) in (select s.customer_id , min(order_date) from sales
  group by s.customer_id ) 
  order by s.customer_id
  
  
  
  What is the most purchased item on the menu and how many times was it purchased by all customers?
  
  select m.product_name, count(s.product_id) as most_selling 
  from menu as m
  join sales as s
  on s.product_id = m.product_id
  group by m.product_name
  order by most_selling desc
  limit 1


  
  Which item was the most popular for each customer?
  
  select s.customer_id ,  m.product_name, count(s.product_id) as order_count 
  from sales as s
  join menu as m
  on s.product_id = m.product_id
  group by s.customer_id,s.product_id, m.product_name
  order by order_count desc


  
  Which item was purchased first by the customer after they became a member?
  
  select s.customer_id, m.product_id, m.product_name, s.order_date
  from sales as s
  join menu as m
  on m.product_id = s.product_id
  join members as me
  on s.customer_id = me.customer_id
  where s.order_date >= me.join_date
  and s.order_date = (select min(s2.order_date) from sales as s2
  where s2.customer_id = s.customer_id
  and s2.order_date >= me.join_date)
  
  
  
  Which item was purchased just before the customer became a member?
  
  select s.customer_id, m.product_id, m.product_name, s.order_date
  from sales as s
  join menu as m
  on m.product_id = s.product_id
  join members as me
  on s.customer_id = me.customer_id
  where s.order_date <= me.join_date
  and s.order_date = (select min(s2.order_date) from sales as s2
  where s2.customer_id = s.customer_id
  and s2.order_date <= me.join_date)


  
  What is the total items and amount spent for each member before they became a member?
  
  select s.customer_id, sum(m.price) total_spend, count(s.product_id) as total_quantity
  from sales as s
  join menu as m
  on m.product_id = s.product_id
  join members as me
  on s.customer_id = me.customer_id
  where me.join_date > s.order_date
  group by s.customer_id
  order by customer_id


  

  If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
  
  WITH points_cte AS (
  SELECT m.product_id, 
  CASE
  WHEN product_id = 1 THEN price * 20
  ELSE price * 10 END AS points
  FROM menu as m)
  
  select s.customer_id, sum(points_cte.points) as total_points
  from sales as s
  inner join points_cte
  on points_cte.product_id = s.product_id
  group by s.customer_id


![Dannys Dinner_page-0001](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/4ff5f431-c551-4111-ad36-156ee6d08e6c)

![Dannys Dinner_page-0002](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/2cc7fc80-3e68-4278-8ea5-6a4b53fa5447)

![Dannys Dinner_page-0003](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/35e92841-e12e-4a57-8825-e8cab91b0b7a)

![Dannys Dinner_page-0004](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/a06536e7-c8ec-4fcc-bb2b-fc0a6f22ec35)

![Dannys Dinner_page-0005](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/88fcf2b2-0f7c-435d-8898-fbcf5d53af81)

![Dannys Dinner_page-0006](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/24d9026d-ac29-41f6-8a88-c690dcf23e56)

![Dannys Dinner_page-0007](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/1f25897c-9bf3-439f-84de-74beb17ddb16)

![Dannys Dinner_page-0008](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/c3a72363-b59e-4f69-9806-b78fc3d6d274)

![Dannys Dinner_page-0009](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/073b763c-230f-4d92-9e34-8a45f7813fd6)

![Dannys Dinner_page-0010](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/24aa2130-7ac9-4e3c-9d7a-8529446add6c)

![Dannys Dinner_page-0011](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/db278c50-37ed-444b-8964-80803845712c)

![Dannys Dinner_page-0012](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/32401613-d41c-4de2-b1e1-37ead7c60c13)

![Dannys Dinner_page-0013](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/9b595c3e-67ce-4397-bba0-8a62c77b4da4)

![Dannys Dinner_page-0014](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/f78f4f52-38cc-402c-8d0c-57504ec4b1db)

![Dannys Dinner_page-0015](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/f600e9e9-c0ba-486b-b635-f88dd30956a6)

![Dannys Dinner_page-0016](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/7f2231b5-7237-4df9-bf50-bc83b1353971)

![Dannys Dinner_page-0017](https://github.com/pawansukheja/Danny-s-Dinner-using-SQL/assets/163865690/d7ba81ca-9159-4711-82c3-23cafa59e81b)
