# Case-Study-2---Pizza-Runner

![image](https://github.com/user-attachments/assets/da89b91d-962d-4af3-86bb-23ae612245af)


## Introduction

- Did you know that over 115 million kilograms of pizza is consumed daily worldwide??? (Well according to Wikipedia anyway…)
- Danny was scrolling through his Instagram feed when something really caught his eye - “80s Retro Styling and Pizza Is The Future!”
- Danny was sold on the idea, but he knew that pizza alone was not going to help him get seed funding to expand his new Pizza Empire - so he had one more genius idea to combine with it - he was going to Uberize it - and so Pizza Runner was launched!
- Danny started by recruiting “runners” to deliver fresh pizza from Pizza Runner Headquarters (otherwise known as Danny’s house) and also maxed out his credit card to pay freelance developers to build a mobile app to accept orders from customers.

## Available Data

- Because Danny had a few years of experience as a data scientist - he was very aware that data collection was going to be critical for his business’ growth.
- He has prepared for us an entity relationship diagram of his database design but requires further assistance to clean his data and apply some basic calculations so he can better direct his runners and optimise Pizza Runner’s operations.
- All datasets exist within the pizza_runner database schema - be sure to include this reference within your SQL scripts as you start exploring the data and answering the case study questions.

  ![image](https://github.com/user-attachments/assets/544a517d-4792-4405-a757-dbb1601bde45)


## Table 1: runners
The runners table shows the registration_date for each new runner

| runner_id | registration_date |
|-----------|-------------------|
| 1         | 2021-01-01        |
| 2         | 2021-01-03        |
| 3         | 2021-01-08        |
| 4         | 2021-01-15        |


## Table 2: customer_orders
- Customer pizza orders are captured in the customer_orders table with 1 row for each individual pizza that is part of the order.
- The pizza_id relates to the type of pizza which was ordered whilst the exclusions are the ingredient_id values which should be removed from the pizza and the extras are the ingredient_id values which need to be added to the pizza.
Note that customers can order multiple pizzas in a single order with varying exclusions and extras values even if the pizza is the same type!
- The exclusions and extras columns will need to be cleaned up before using them in your queries.

| order_id | customer_id | pizza_id | null | extras | order_time      |
|----------|-------------|----------|------|--------|-----------------|
| 1        | 101         | 1        | null | null   | 1/1/2021 18:05  |
| 2        | 101         | 1        | null | null   | 1/1/2021 19:00  |
| 3        | 102         | 1        | null | null   | 1/2/2021 23:51  |
| 3        | 102         | 2        | null | NaN    | 1/2/2021 23:51  |
| 4        | 103         | 1        | 4    | null   | 1/4/2021 13:23  |
| 4        | 103         | 1        | 4    | null   | 1/4/2021 13:23  |
| 4        | 103         | 2        | 4    | null   | 1/4/2021 13:23  |
| 5        | 104         | 1        | null | 1      | 1/8/2021 21:00  |
| 6        | 101         | 2        | null | null   | 1/8/2021 21:03  |
| 7        | 105         | 2        | null | 1      | 1/8/2021 21:20  |
| 8        | 102         | 1        | null | null   | 1/9/2021 23:54  |
| 9        | 103         | 1        | 4    | 1, 5   | 1/10/2021 11:22 |
| 10       | 104         | 1        | null | null   | 1/11/2021 18:34 |
| 10       | 104         | 1        | 2, 6 | 1, 4   | 1/11/2021 18:34 |



## Table 3: runner_orders
- After each orders are received through the system - they are assigned to a runner - however not all orders are fully completed and can be cancelled by the restaurant or the customer.
- The pickup_time is the timestamp at which the runner arrives at the Pizza Runner headquarters to pick up the freshly cooked pizzas. The distance and duration fields are related to how far and long the runner had to travel to deliver the order to the respective customer.
- There are some known data issues with this table so be careful when using this in your queries - make sure to check the data types for each column in the schema SQL!

| order_id | runner_id | pickup_time         | distance | duration   | cancellation            |
|----------|-----------|---------------------|----------|------------|-------------------------|
| 1        | 1         | 2021-01-01 18:15:34 | 20km     | 32 minutes |                         |
| 2        | 1         | 2021-01-01 19:10:54 | 20km     | 27 minutes |                         |
| 3        | 1         | 2021-01-03 00:12:37 | 13.4km   | 20 mins    | NaN                     |
| 4        | 2         | 2021-01-04 13:53:03 | 23.4     | 40         | NaN                     |
| 5        | 3         | 2021-01-08 21:10:57 | 10       | 15         | NaN                     |
| 6        | 3         | null                | null     | null       | Restaurant Cancellation |
| 7        | 2         | 2020-01-08 21:30:45 | 25km     | 25mins     | null                    |
| 8        | 2         | 2020-01-10 00:15:02 | 23.4 km  | 15 minute  | null                    |
| 9        | 2         | null                | null     | null       | Customer Cancellation   |
| 10       | 1         | 2020-01-11 18:50:20 | 10km     | 10minutes  | null                    |


## Table 4: pizza_names
At the moment - Pizza Runner only has 2 pizzas available the Meat Lovers or Vegetarian!


| pizza_id | pizza_name  |
|----------|-------------|
| 1        | Meat Lovers |
| 2        | Vegetarian  |


## Table 5: pizza_recipes
Each pizza_id has a standard set of toppings which are used as part of the pizza recipe.

| pizza_id	toppings |   |   |   |    |    |   |    |
|-------------------|---|---|---|----|----|---|----|
| 1	1               | 2 | 3 | 4 | 5  | 6  | 8 | 10 |
| 2	4               | 6 | 7 | 9 | 11 | 12 |   |    |


## Table 6: pizza_toppings
This table contains all of the topping_name values with their corresponding topping_id value

| topping_id | topping_name |
|------------|--------------|
| 1          | Bacon        |
| 2          | BBQ Sauce    |
| 3          | Beef         |
| 4          | Cheese       |
| 5          | Chicken      |
| 6          | Mushrooms    |
| 7          | Onions       |
| 8          | Pepperoni    |
| 9          | Peppers      |
| 10         | Salami       |
| 11         | Tomatoes     |
| 12         | Tomato Sauce |


## Schema

```sql
CREATE SCHEMA pizza_runner;
SET search_path = pizza_runner;

DROP TABLE IF EXISTS runners;
CREATE TABLE runners (
  "runner_id" INTEGER,
  "registration_date" DATE
);
INSERT INTO runners
  ("runner_id", "registration_date")
VALUES
  (1, '2021-01-01'),
  (2, '2021-01-03'),
  (3, '2021-01-08'),
  (4, '2021-01-15');


DROP TABLE IF EXISTS customer_orders;
CREATE TABLE customer_orders (
  "order_id" INTEGER,
  "customer_id" INTEGER,
  "pizza_id" INTEGER,
  "exclusions" VARCHAR(4),
  "extras" VARCHAR(4),
  "order_time" TIMESTAMP
);

INSERT INTO customer_orders
  ("order_id", "customer_id", "pizza_id", "exclusions", "extras", "order_time")
VALUES
  ('1', '101', '1', '', '', '2020-01-01 18:05:02'),
  ('2', '101', '1', '', '', '2020-01-01 19:00:52'),
  ('3', '102', '1', '', '', '2020-01-02 23:51:23'),
  ('3', '102', '2', '', NULL, '2020-01-02 23:51:23'),
  ('4', '103', '1', '4', '', '2020-01-04 13:23:46'),
  ('4', '103', '1', '4', '', '2020-01-04 13:23:46'),
  ('4', '103', '2', '4', '', '2020-01-04 13:23:46'),
  ('5', '104', '1', 'null', '1', '2020-01-08 21:00:29'),
  ('6', '101', '2', 'null', 'null', '2020-01-08 21:03:13'),
  ('7', '105', '2', 'null', '1', '2020-01-08 21:20:29'),
  ('8', '102', '1', 'null', 'null', '2020-01-09 23:54:33'),
  ('9', '103', '1', '4', '1, 5', '2020-01-10 11:22:59'),
  ('10', '104', '1', 'null', 'null', '2020-01-11 18:34:49'),
  ('10', '104', '1', '2, 6', '1, 4', '2020-01-11 18:34:49');


DROP TABLE IF EXISTS runner_orders;
CREATE TABLE runner_orders (
  "order_id" INTEGER,
  "runner_id" INTEGER,
  "pickup_time" VARCHAR(19),
  "distance" VARCHAR(7),
  "duration" VARCHAR(10),
  "cancellation" VARCHAR(23)
);

INSERT INTO runner_orders
  ("order_id", "runner_id", "pickup_time", "distance", "duration", "cancellation")
VALUES
  ('1', '1', '2020-01-01 18:15:34', '20km', '32 minutes', ''),
  ('2', '1', '2020-01-01 19:10:54', '20km', '27 minutes', ''),
  ('3', '1', '2020-01-03 00:12:37', '13.4km', '20 mins', NULL),
  ('4', '2', '2020-01-04 13:53:03', '23.4', '40', NULL),
  ('5', '3', '2020-01-08 21:10:57', '10', '15', NULL),
  ('6', '3', 'null', 'null', 'null', 'Restaurant Cancellation'),
  ('7', '2', '2020-01-08 21:30:45', '25km', '25mins', 'null'),
  ('8', '2', '2020-01-10 00:15:02', '23.4 km', '15 minute', 'null'),
  ('9', '2', 'null', 'null', 'null', 'Customer Cancellation'),
  ('10', '1', '2020-01-11 18:50:20', '10km', '10minutes', 'null');


DROP TABLE IF EXISTS pizza_names;
CREATE TABLE pizza_names (
  "pizza_id" INTEGER,
  "pizza_name" TEXT
);
INSERT INTO pizza_names
  ("pizza_id", "pizza_name")
VALUES
  (1, 'Meatlovers'),
  (2, 'Vegetarian');


DROP TABLE IF EXISTS pizza_recipes;
CREATE TABLE pizza_recipes (
  "pizza_id" INTEGER,
  "toppings" TEXT
);
INSERT INTO pizza_recipes
  ("pizza_id", "toppings")
VALUES
  (1, '1, 2, 3, 4, 5, 6, 8, 10'),
  (2, '4, 6, 7, 9, 11, 12');


DROP TABLE IF EXISTS pizza_toppings;
CREATE TABLE pizza_toppings (
  "topping_id" INTEGER,
  "topping_name" TEXT
);
INSERT INTO pizza_toppings
  ("topping_id", "topping_name")
VALUES
  (1, 'Bacon'),
  (2, 'BBQ Sauce'),
  (3, 'Beef'),
  (4, 'Cheese'),
  (5, 'Chicken'),
  (6, 'Mushrooms'),
  (7, 'Onions'),
  (8, 'Pepperoni'),
  (9, 'Peppers'),
  (10, 'Salami'),
  (11, 'Tomatoes'),
  (12, 'Tomato Sauce');
```


## Case Study Questions

- Pizza Metrics
- Runner and Customer Experience
- Ingredient Optimisation
- Pricing and Ratings
- Bonus DML Challenges (DML = Data Manipulation Language)


### A. Pizza Metrics

1. How many pizzas were ordered?

```Sql
Select
      count(pizza_id) as pizza_order_count
From
      customer_orders;
```

![image](https://github.com/user-attachments/assets/f64fbe68-f274-42b5-86fd-b37c5b08b93e)

- Total of 14 Pizzas were ordered by 5 customers with 10 order_ids

2. How many unique customer orders were made?

```sql
select count(distinct(order_id))
From customer_orders;
```

![image](https://github.com/user-attachments/assets/7869b588-88b2-4959-99c3-7c74ac83b58e)


- Total of 10 Unique customer orders were made.

3. How many successful orders were delivered by each runner?
```sql
SELECT runner_id,count(*) as successful_orders
FROM runner_orders
WHERE cancellation IS NULL OR cancellation NOT LIKE '%Cancellation%'
Group by runner_id
order by runner_id;
```

![image](https://github.com/user-attachments/assets/675502d4-26dc-443a-b4e2-85b8676b4780)

- Total 8 orders were successfully delivered by runners.
- 2 orders were cancelled. One by Restaurant and other by customer.
- Runner 1 delivered 4 orders.
- Runner 2 delivered 3 orders.
- Runner 3 delivered 1 order.
  
4. How many of each type of pizza was delivered?
```sql
select p.pizza_name,count(*) as pizza_type_count 
from customer_orders c
join runner_orders r
using(order_id)
join pizza_names p
using(pizza_id)
WHERE r.cancellation IS NULL OR r.cancellation NOT LIKE '%Cancellation%'
group by p.pizza_name,c.pizza_id;
```

  ![image](https://github.com/user-attachments/assets/b3058161-1ab7-4e78-8a5b-904c72f94427)

- Total 14 pizzas were ordered. Out of 14, 12 got delivered.
- 9 Meatlovers were delivered
- 3 Vegetarian were delivered

5. How many Vegetarian and Meatlovers were ordered by each customer?
```sql
select customer_id,pizza_name,count(pizza_id) from customer_orders c
join pizza_names p
using(pizza_id)
Group by 1,2
order by 1,2;
```

![image](https://github.com/user-attachments/assets/3392d6d0-c805-4b79-8fef-9b3bedda7eda)

- Total 14 pizzas were ordered by customers
- Out of which customer 101 ordered 2 Meatlovers and 1 vegetarian.
- Out of which customer 102 ordered 2 Meatlovers and 1 vegetarian.
- Out of which customer 103 ordered 3 Meatlovers and 1 vegetarian.
- Out of which customer 104 ordered 3 Meatlovers. 
- Out of which customer 105 ordered 1 vegetarian.

6. What was the maximum number of pizzas delivered in a single order?

```sql
select c.order_id,count(*) as max_pizza_delivered from customer_orders c
join runner_orders r
using(order_id)
WHERE r.cancellation IS NULL OR r.cancellation NOT LIKE '%Cancellation%'
Group by 1
order by 2 desc
limit 1;
```

![image](https://github.com/user-attachments/assets/fdcdc988-cd86-4702-a972-c53f287f85f7)

- 3 pizza were delivered under order_id 4

7. For each customer, how many delivered pizzas had at least 1 change and how many had no changes?


8. How many pizzas were delivered that had both exclusions and extras?
9. What was the total volume of pizzas ordered for each hour of the day?
10. What was the volume of orders for each day of the week?




