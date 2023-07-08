# Sales-Analysis-Atliq-Hardware
![PinClipart com_now-hiring-clipart_5313368-overlay](https://github.com/Shreya007data/Sales-Analysis-Atliq-Hardware/assets/132162991/d5aa24b1-c7cf-4ee4-9f57-0c2ab7a8bdfe)





## INTRODUCTION 

In this project, I have discovered the captivating sales insights of an India-based Hardware peripherals Company : **AtliQ Hardware**. It is a data analysis project that unveils customer behavior, market trends, and business performance through powerful Data Analysis and Visualisation.

## PROBLEM STATEMENT 

AtliQ Hardware supplies computer hardware and peripherals to many clients across India, such as surge stores, Nomad stores, etc. AtliQ Hardware's head office is in Delhi, India and has many regional offices throughout India. They have regional managers for North, South and Central India. The market is growing dynamically but the sales are declining for the company and the sales director is having issues tracking the sales and what is actually happening at a ground level that the business is actually failing.

The company wants a simple data visualization tool that they can access on a daily basis. By using that tools and technology they can make data driven decisions that help them to boost the sales for the company. So, In this project, I have helped AtliQ Hardware by making their own sales dashboard using **Power BI** for decision support & automating the process.

 ## PROJECT PLANNING USING AIMS GRID 
 
**1. Purpose :-**  To unlock sales insights that are not visible before the sales team for decision support and automate them to reduce manual time spent in data gathering.

**2. Stakeholders :-**
-   Sales Director
-   Marketing Team
-   Customer Service Team
-   Data and Analytics Team
-   IT

**3. End result :-**  An automated dashboard providing quick and latest sights in order to support data driven decision making.

**4. Success Criteria :-**
-   Dashboard uncovering sales order insights with the latest data available.
-   Sales team able to take better decisions and prove 10% cost saving of total spend.
-   Sales analysis stops data gathering manually in order to save 20% business time and reinvested it in any other value added activity.

## DATA ANALYSIS : MY SQL 

- Imported data into MY SQL Workbench for Data Analysis

![233262064-b1fb8f0f-8c16-402d-adac-07784b81a2fe](https://github.com/Shreya007data/Sales-Analysis-Atliq-Hardware/assets/132162991/d4207ffe-d52c-4656-97ac-79fddfb558f3)


- Queries for further data analysis -
  
 1.  To find all customers records
    
```SQL
SELECT * FROM sales.customers;
```


2. To find transactions for the Chennai market (market code for Chennai is Mark001)
```SQL
SELECT * FROM sales.transactions where market_code='Mark001';
```

3. To find distinct product codes that were sold in Mumbai
```SQL
SELECT distinct product_code FROM sales.transactions where market_code='Mark002';
```
4. To find transactions where the currency is US dollars
```SQL
SELECT * from sales.transactions where currency="USD";
```
5. To find transactions in 2020 join by date table
```SQL
SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020;`
```

6. To find the total revenue for the year 2020
```SQL
SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r";
```



7. To find the total revenue for January, 2019
```SQL
SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="January" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");
```


8. To find total revenue for Chennai in the year 2020 
```SQL
SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.market_code="Mark001";
```

##  DATA CLEANING & ETL : POWER BI

In this process, I have done data cleaning and ETL using **Power Bi** - 

Step 1: Connected the MySQL database with the Power Bi desktop.

Step 2: Loaded data into the Power BI desktop. This step imported all the tables and creates a database. 

Step 3: Transform data with the help of Power Query

Perform filtration in Markets table: In the table markets when we click on the transform data option, we are directed to Power query editor. Power Query editor is where we perform out ETL and then we can perform data transformation i.e. Data Cleaning, Data Wrangling, and Data Munging. we need to filter the rows where the values are null and filter the data and deselect the blank option.

Perform filtration in Transactions table: In the Transactions table when we filter negative values and  0 values that appear in the table, the desired output is received then, we deselect all the garbage values.

Convert USD into INR in the Transactions table: The AtliQ Hardware only works in India so the USD values in the transactions table need to be converted into INR by using some formulas. First, we will add a Conditional column then, normalized currency where sales amount will be in INR 

In the power query editor, we will write this formula for converting the USD currency into INR -
```
 = Table.AddColumn(#"Filtered Rows", "norm_sales_amount",each if [currency] = "USD" then [sales_amount]*75 else [sales_amount]`

```



In MySQL Workbench there are duplicates of USD and INR , to find duplicates we will write these formulaes -

 
```
 SELECT count(*) from sales.transactions where sales.transactions.currency="INR";

 SELECT count(*) from sales.transactions where  sales.transactions.currency="USD";

 SELECT * from sales.transactions where sales.transactions.currency='USD\r' or sales.transactions.currency='USD';`

```
The USD And INR have duplicates and for analysis, it is better to delete these duplicates of them. So, I have deleted USD and kept USD/r so with INR.  

##   DAX MEASURE

The Dax Measure  which I used in my visualization are:
-   Revenue =  `SUM('sales transactions'[sales_amount])`
-   Sales quantity =  `SUM('sales transactions'[sales_qty])`

## SALES DASHBOARD 

I have visualized the entire dataset of AtliQ Hardware using Power Bi to know what the numbers in and behind the data want to convey. I have created a dashboard for the same using different statistical graphs and diagrams for unveiling the sales insights of the company.


https://github.com/Shreya007data/Sales-Analysis-Atliq-Hardware/assets/132162991/448736b2-1be2-4d11-9033-acfe68da7256

## RECOMMENDATIONS
Based on the dashboard insights, I have made some recommendations to the Sales & Marketing team that they can follow to boost Sales -

1) Consider making a sales strategy for especially Lucknow since it's showing the lowest revenue and negative profit margin and if possible so as for Surat and Bhubhaneshwar also.
2) Try to increase its sales quantity in Patna, Surat and Kanpur since they have the lowest sales quantity.
3) Start target campaign for Prod047 and Prod061 since they two are the most profitable selling products.
4) Try to give special benefits to Electronics and Excel stores as they are their most profitable customers.
5) Make their campaign strategy for mid-year as they are showing high sales among other months.
