

### Data Analysis Using SQL



1- To find all customers records

  SELECT * FROM sales.customers;


2- To find transactions for the Chennai market (market code for Chennai is Mark001)

    SELECT * FROM sales.transactions where market_code='Mark001';


3- To find distinct product codes that were sold in Mumbai

SELECT distinct product_code FROM sales.transactions where market_code='Mark002';


4- To find transactions where the currency is US dollars

SELECT * from sales.transactions where currency="USD";


5- To find transactions in 2020 join by date table

SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020;


6- To find the total revenue for the year 2020

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 
and sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r";


7- To find the total revenue for January, 2019

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="January" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");


8- To find total revenue for Chennai in the year 2020

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.market_code="Mark001";