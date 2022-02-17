# A project containing data on healthy eating 

## Table A: SQL_4_food_eng 

 This table contains columns and records. It concerns the calorific value of products in 100g. 

### Columns:  

**Product name**  
**type**: fruit, vegetable, grains, dairy products, canned food, meat, fish, spices, seeds, other.  
**calories**  
**proteins**  
**lipids**  
**carbohydrates**  

Definition of the Table can look like that:

``` sql
CREATE TABLE "SQL_4_food_eng" (
	"product_name"	TEXT UNIQUE,
	"type"	TEXT,
	"calories"	INTEGER,
	"proteins"	INTEGER,
	"lipids"	INTEGER,
	"carbohydrates"	INTEGER,
	PRIMARY KEY("product_name")
)
```

### Product examples (column: product_name   

* amaranth
* pineapple
* broccoli 
* clove
* salmon
* sugar
* natural yogurt
* rye bread
* dry smoked pork sausage
* chicken breast
* sesame
* corn
* cinnamon
* strawberries
* corn flour
* red kidney bean
* ginger
* honey
* cottage cheese
* codfish


## Table B: product_price  

This table contains data on the price of 100g for a specific product and calories. There are 3 columns in it:
**product_name** and **price_PLN_for_100g** and **calories**:

Definition:

``` sql
CREATE TABLE "product_price" (
	"product_name"	TEXT UNIQUE,
	"price_PLN_for_100g"	INTEGER,
	"calories"	INTEGER,
	PRIMARY KEY("product_name")
);
```

# SQL queries

In the database **SQL_4_food_eng**, you can perform example SQL queries: 

## Examples for SELECT

* SELECT showing the names of all products belonging to the type "fruit": 

```sql
SELECT product_name FROM SQL_4_food_eng WHERE type = "fruit";
```

* SELECT showing the names of all products belonging to the type "vegetable":

```sql
SELECT product_name FROM SQL_4_food_eng WHERE type = "vegetable"; 
```

* SELECT showing the type of vegetable and all vegetable products with less than 70 calories: 

``` sql
SELECT product_name FROM SQL_4_food_eng WHERE type = "vegetable" AND calories <= 70; 
```

* SELECT that displays the name of the product based on certain parameters: type = "seeds" and proteins <= 5 and lipids <= 1.2 (three conditions must be met):

``` sql
SELECT product_name FROM SQL_4_food_eng WHERE type = "seeds" AND proteins <= 5 AND lipids <= 1.2; 
```

* SELECT showing names of all products including proteins equal to or greater than 10: 

``` sql
SELECT product_name FROM SQL_4_food_eng WHERE proteins >= 10; 
```

* SELECT that displays sample calculations for calories, proteins, and lipids and their corresponding aliases: 

``` sql
SELECT calories + 2 AS Gladiator,
proteins - 1 AS Maximus,
lipids * (12 + carbohydrates/4) AS Kate
FROM SQL_4_food_eng;
```

* SELECT which is displaying all product names and type, and the corresponding calories, proteins, carbohydrates and lipids calculations:

``` sql
SELECT product_name, type, (calories * proteins) + (carbohydrates-lipids) FROM SQL_4_food_eng; 
```

* SELECT showing names of all products with calories <= 200: 

``` sql
SELECT product_name, calories FROM SQL_4_food_eng WHERE calories <= 200; 
```

 * SELECT which is displaying the names of all products assigned as alias "low calorie products" in the range calories <= 200:
 
``` sql
SELECT product_name AS "low calorie products" FROM SQL_4_food_eng WHERE calories <= 200; 
```

* SELECT which is displaying names of all canned products containing calories <= 100: 

``` sql
SELECT product_name FROM SQL_4_food_eng WHERE type = "canned food" AND calories <= 100; 
```

* SELECT which is displaying names of all products of the fruit type containing calories <= 50: 

``` sql
SELECT product_name FROM SQL_4_food_eng WHERE type = "fruit" AND calories <= 50; 
```

* SELECT displaying names of all products with proteins <= 10: 

``` sql
SELECT product_name FROM SQL_4_food_eng WHERE "proteins" <= 10; 
```

## Example for DELETE

* displaying record 0 and deleting this one record: 

``` sql
SELECT product_name FROM SQL_4_food_eng WHERE product_name = "0"; 
```

``` sql
DELETE FROM SQL_4_food_eng WHERE product_name = "0";
```
Removal of the product named "cherry". It is a good practice to check an existing record first - this is how you can check the WHERE clause: 

``` sql
SELECT product_name FROM SQL_4_food_eng WHERE product_name = "ginger"; 
```

``` sql
DELETE FROM SQL_4_food_eng WHERE product_name = "ginger"; 
```

Show products with missing data for "type" and "carbohydrates": 

``` sql
SELECT type, calories, proteins, lipids, carbohydrates
FROM SQL_4_food_eng
WHERE type IS NULL AND carbohydrates IS NULL;
```

Nested SELECT and DELETE which will check and delete data which equals 0 or NULL:

``` sql
SELECT * FROM SQL_4_food_eng WHERE (type IS NULL AND carbohydrates IS NULL) OR (product_name = '0' AND type = '0' AND calories= '0' AND proteins = '0' AND lipids = '0' AND carbohydrates = '0 '); 
```

``` sql
DELETE FROM SQL_4_food_eng WHERE (type IS NULL AND carbohydrates IS NULL) OR (product_name = '0' AND type = '0' AND calories= '0' AND proteins = '0' AND lipids = '0' AND carbohydrates = '0' ) 
```

## Example - DELETE and INSERT

Checking for the existence of a product named "orbit_gum": 

``` sql
SELECT product_name FROM SQL_4_food_eng WHERE product_name = "orbit_gum";
```
Removal of the product "orbit_gum: 

``` sql
DELETE FROM SQL_4_food_eng WHERE product_name = "orbit_gum"; 
```

Added product "orbit_gum": 

``` sql
INSERT INTO SQL_4_food_eng (product_name, type, calories, proteins, lipids, carbohydrates) VALUES ("orbit_gum", "other", "50", "3", "2", "10");
```

To add multiple rows to a table at once, I use the following form of the INSERT statement:

``` sql
INSERT INTO SQL_4_food_eng (product_name, type, calories, proteins, lipids, carbohydrates) VALUES 
("pumpkin_seeds", "seeds", "572", "24.5", "45.8", "18"), ("pears", "fruit", "58", "0.38", "0.12", "15.4"), 
("carrots", "vegetable", "41", "1", "0", "10");
```

We can check WHERE clausule with SELECT:

``` sql
SELECT product_name FROM SQL_4_food_eng WHERE product_name = "pumpkin_seeds"; 
```

``` sql
DELETE FROM SQL_4_food_eng WHERE product_name = "pumpkin_seeds";
```

## Example - UPDATE 

Changing an existing record for "orbit_gum".
First, we check the current state of the data: 

``` sql
SELECT * FROM SQL_4_food_eng WHERE product_name = "orbit_gum"; 
```

After that, we can update the existing data: 

``` sql
UPDATE SQL_4_food_eng SET proteins = "4", calories = "55" WHERE product_name = "orbit_gum";
SELECT * FROM SQL_4_food_eng WHERE product_name = "orbit_gum";
UPDATE SQL_4_food_eng SET proteins = "3", calories = "50" WHERE product_name = "orbit_gum";
SELECT * FROM SQL_4_food_eng WHERE product_name = "orbit_gum";
```

## Example - INNER JOIN SELECT 

The INNER JOIN keyword selects records that have matching values in mentioned tables.

``` sql
SELECT SQL_4_food_eng.product_name, SQL_4_food_eng.calories FROM SQL_4_food_eng
INNER JOIN product_price
ON SQL_4_food_eng.product_name = product_price.product_name;
```

``` sql
SELECT product_price.product_name, product_price.calories FROM product_price
INNER JOIN SQL_4_food_eng
ON product_price.product_name = SQL_4_food_eng.product_name;
```

## Example - LEFT JOIN

The LEFT JOIN query returns all records from the left table (table A) and the matching records from the right table (table B). The result is 0 records from the right side (if there is no match).

``` sql
SELECT SQL_4_food_eng.calories as KCAL_S4F, product_price.calories AS KCAL_CP
FROM SQL_4_food_eng
LEFT JOIN product_price
ON SQL_4_food_eng.calories = product_price.calories;
```

