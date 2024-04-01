# Pizza sales analysis

### Project review 
- This  data analysis project aim to provide insight into sales performance  of a sales company over the pass years
by analyzing various aspect of the company sales data , we seek to identify trend, make data driven recommendation, and gain deeper understaning of the company performance.


### Data Source
Sales Data: The primary dataset used or this analysis is the 'sales_data_csv' which contain vital information about the company sales .

### Tools 
- Excel- Data Cleaning 
- Mysql - Data Analysis
- Power Bi - Creating Report

### Data Cleaning/Preparation
- In the data  cleaning and preparation phase of the project we performed the following task
- Data loading and inspection of the data
- Handling of missing data
- Data cleaning and formating



### Explorative Analysis
- EDA this involved exploring the Sales data to answer some key question.



### Data Analysis 
- mysql
- writing query to answer some question
```mysql
- SELECT * FROM pizza_sales;
```
- Count the number of transaction
 ```mysql
SELECT COUNT(*) FROM pizza_sales;
 ``` 
- Total Revenue
```mysql
SELECT  cast(sum(total_price) as Decimal(10,2))  as Total_revenue from pizza_sales;
 ``` 
- Average Total Revenue
```mysql
Select cast(sum(total_price)/ count(DISTINCT(order_id))as DECIMAL(10,2)) as average_revenue  from pizza_sales;
 ``` 

- Total Quatity of pizza sold
```mysql
SELECT sum(quantity) as total_quantity FROM pizza_sales;
 ``` 

- Total quantity of pizza sold base on size
 ```mysql
SELECT count(quantity) as count , pizza_size  FROM pizza_sales
GROUP BY pizza_size;
 ``` 

- Total pizza sold base on category
```mysql
SELECT count(quantity) as count , pizza_category FROM pizza_sales
GROUP BY  pizza_category;
 ``` 

- Toatl pizza sold base on the size and the category
```mysql
SELECT  count(quantity) as count , pizza_category , pizza_size as size  FROM pizza_sales
GROUP BY pizza_category, pizza_size
ORDER BY count  DESC ;
 ``` 


- Top 5 pizza sold base on size and category
```mysql 
SELECT  count(quantity) as count , pizza_category , pizza_size as size  FROM pizza_sales
GROUP BY pizza_category, pizza_size
ORDER BY count  desc limit 5;
 ``` 

- Bottom  5 pizza sold base on size and category
```mysql 
SELECT  count(quantity) as count , pizza_category , pizza_size as size  FROM pizza_sales
GROUP BY pizza_category, pizza_size
ORDER BY count  asc limit 5;
 ``` 

- Total order of pizza
```mysql
SELECT count(order_id) as total_order FROM pizza_sales;
 ``` 

- Average order of pizza_sales
```mysql
SELECT (sum(quantity)/ count(DISTINCT(order_id))) as average_order FROM pizza_sales;
 ``` 

- To check the date type of the column
```mysql
describe pizza_sales;
 ``` 


- Change  the date type of the column to date 
```mysql
update pizza_sales
set order_date = str_to_date(order_date,'%d-%m-%Y');
 ``` 

- Change the datetype of the order_date column
```mysql
ALTER TABLE pizza_sales
MODIFY COLUMN  order_date DATE ;
 ``` 

- Daily trend of total orders of pizza
```mysql
select  dayname( order_date) as daysofweek , count(DISTINCT(order_id))  as count from pizza_sales
group by daysofweek
order by count desc ;
``` 
- Daily trend of size of pizza
 ```mysql 
select  dayname( order_date) as daysofweek , 
count(DISTINCT(order_id))  as count,
pizza_size as size from pizza_sales
group by daysofweek, size
order by count desc ;
 ``` 

- Dayof week with the higest sale of large pizza size
```mysql
select  dayname( order_date) as daysofweek , 
count(DISTINCT(order_id))  as count,
pizza_size  from pizza_sales
where pizza_size='l'
group by daysofweek, pizza_size
order by count desc;
 ``` 

- Monthly trend of pizza sales
```mysql
select monthname(order_date) as dayofmonth, count(DISTINCT(order_id)) AS COUNT
from pizza_sales
group by dayofmonth
order by count;
 ``` 

- Top 5 month with the higest sales
```mysql
select monthname(order_date) as dayofmonth, count(DISTINCT(order_id)) AS COUNT
from pizza_sales
group by dayofmonth
order by count limit 5;
 ``` 

- The trend  of day and month with the higest sale of pizza
```mysql
select monthname(order_date) as dayofmonth,dayname(order_date) as dayofday, count(DISTINCT(order_id)) AS COUNT
from pizza_sales
group by dayofmonth, dayofday
order by count desc ;
 ``` 

- %Sale of pizza by category
 ```mysql
select pizza_category, cast(sum(total_price) as decimal(10,2)) as total_revenue,
cast((sum(total_price)*100)as decimal(10,2))/( select sum(total_price) from pizza_sales) as percentage  from pizza_sales
GROUP BY pizza_category;
 ``` 

- %Change of sale of pizza with size
 ```mysql
select pizza_size, cast(sum(total_price) as decimal(10,2)) as total_revenue,
cast((sum(total_price)*100)as decimal(10,2))/( select sum(total_price) from pizza_sales) as percentage  from pizza_sales
GROUP BY pizza_size
order by pizza_size;
 ``` 
- The time of the day with the higest sale of pizza
 ```mysql
select dayname(order_date) as days , hour(order_time) as time ,count(distinct(order_id)) as count,
sum(quantity) as quantity_sold 
from pizza_sales
group by days, time 
order by count desc ;
 ``` 

- Top five pizza revenue
 ```mysql
select  sum(total_price) , pizza_category from pizza_sales
group by pizza_category;
 ``` 

- Top five pizza name  by quantity
 ```mysql 
select pizza_name, sum(quantity) as quantity  from pizza_sales
group by pizza_name
order by quantity desc  limit 5;
  ``` 

- Pizza name with the higest sales
```mysql
select cast( sum(total_price)as decimal(10,4))as total_revenue , pizza_name  from pizza_sales
group by pizza_name
order by total_revenue limit 5 ;
 ``` 

- Pizza with the lowet sales
 ```mysql
select cast( sum(total_price)as decimal(10,4))as total_revenue , pizza_name  from pizza_sales
group by pizza_name
order by total_revenue asc limit 5;
 ``` 

- What category of pizza have the higest sale  by pizza name
``` mysql
select pizza_category, count(total_price), pizza_name
from pizza_sales
group by pizza_category, pizza_name
order by count(total_price) DESC limit 5;
 ``` 


- Pissa name with the higest order
```mysql
select count(order_id) as total_orders , pizza_name as name  from pizza_sales
group by pizza_name
order by total_orders desc ;
 ``` 

- Pizza size with the max price
```mysql
select max(total_price)  as total_revenue , pizza_size
from pizza_sales
group by pizza_size;
 ``` 



- The max amount for class pizza from all size and category
 ``` mysql
select max(total_price)  as total_revenue , pizza_size, pizza_category
from pizza_sales
where pizza_category= 'classic'
group by pizza_size, pizza_category
order by total_revenue desc
 ```

### Power Bi
- Load data into Power BI Desktop, dataset is a csv file.
- Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- It was observed that in none of the columns errors & empty values were presented
- in the report view a canvans backgroud is imported into the report view.
- creating of date table
- Data modeling with  sales data table
- calculation of key matric with virtuel card
- ploting  graphs




### Result/Findings
The analysis result are summarize as folllows:
- The pizza  sales have being incresing over the past years  with a noticeable peak during the weekend.
- pizza category classic have the higgest sales
-  pizza size(l) have the higest sales while pizza size(xxl) make minimum sales
- pzza sale increase over the month with the higest sale during july



### Recommendation 
Base on the analysis we recommend the follwing actions:
- invest in marketing and promotion  during peaks sales season to maximize profit and revenue
- focus on expaning and promoting pizza size(xxl) to increase sales

## Image

![image](![Screenshot (105) pngruk](https://github.com/Indeedelight12345/Sales_analysis/assets/159934989/95285eeb-6ea5-493e-96d5-808c2eec3abe)
)



















