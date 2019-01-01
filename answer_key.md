---
output:
  pdf_document: default
  html_document: default
---

# SQL class answer key
# Date: 2018-12-21
# Author: Chao Wang



# 1.1 Find all the infomation about wines in drinkInfo
```{SQL}
SELECT *
FROM drinkInfo
WHERE type = "wine”;
```

# 1.2 Find all the drinkIds of beer
```{SQL}
SELECT drinkId
FROM drinkInfo
WHERE type = "beer";
```

# 1.3 Find what types of drinks are on the menu
```{SQL}
SELECT DISTINCT type
FROM drinkInfo;
```

# 1.4 Find all the orders from person 2
```{SQL}
SELECT *
FROM Orders
WHERE person = "person 2";
```

# 1.5 Find All orders from person 2, arrange by date
```{SQL}
SELECT *
FROM Orders
WHERE person = "person 2"
ORDER BY date;
```

# 1.6 Find how many drinks do each person ordered
```{SQL}
SELECT person, sum(quantity) as total_q
FROM Orders
GROUP BY person;
```

# 1.7 Find the cheapest drink
```{SQL}
SELECT drinkId, MIN(price) AS the_cheapest_drink
FROM HasOnMenu;
```

# 1.8 Find the first 5 rows of `HasOnMenu`
```{SQL}
SELECT *
FROM HasOnMenu
LIMIT 5;
```

# 1.9 Find the average price by bar, order it from high to low
```{SQL}
SELECT bar, AVG(price)
FROM HasOnMenu
GROUP BY bar
ORDER BY AVG(price) DESC;
```

# 1.10 Find all the drinks that are either rum of whisky
```{SQL}
SELECT *
FROM drinkInfo
WHERE type = "rum" OR type = "whisky";
```

# Lesson2
#1.11 Review Exercise Retrieve the bar name and the average price of each bar. Order the results from the most expensive to the cheapest bar.
```{SQL}
SELECT bar, AVG(price) as avg_price
FROM hasonmenu
GROUP BY bar
ORDER BY avg_price DESC;
```

#1.12 Find the price difference between the most expensive drink and the cheapest drink in bar 1 using HasOnMenu table
```{SQL}
SELECT MAX(price)-MIN(price)AS Price_Difference
FROM HasOnMenu
WHERE bar = "bar 1";
```

#1.13 Find the type of drinks that have more than 8 different drinkIds in drinkInfo(HAVING)
```{SQL}
SELECT type, count(drinkId) as quant
FROM drinkInfo
GROUP BY type
HAVING quant > 8;
```
#1.14 Find drink types with an ‘a’
```{SQL}
SELECT *
FROM drinkInfo
WHERE type LIKE "%a%";
```
#1.15 Find all the drinks that are either rum of whisky
```{SQL}
SELECT *
FROM drinkInfo
WHERE type = "rum" OR type="whisky";
```

#1.16 Find all the orders made by person 1, along with the drink types (Writing it with a WHERE clause)
```{SQL}
SELECT person, date, bar, D.drinkId, quantity, type
FROM Orders O, drinkInfo D
WHERE O.drinkId = D.drinkId AND person = "person 1";
```

#1.17 Find all the orders made by person 1, along with the drink types (Writing it with an INNER JOIN clause)
```{SQL}
SELECT person, date, bar, D.drinkId, quantity, type
FROM Orders O
INNER JOIN drinkInfo D
ON O.drinkId = D.drinkId
WHERE person = "person 1”;
```

#1.18 Which bar sells the cheapest drink? What drink is that? What type of drink it is? What is the the price?
```{SQL}
SELECT bar, drinkID, type, MIN(price)
FROM HasOnMenu H
JOIN drinkInfo D
ON D.drinkId = H.drinkId;
```

#1.19 Find all the pairs of soda's drinkIds
```{SQL}
SELECT D1.drinkId AS drink1, D2.drinkId AS drink2
FROM drinkInfo D1, drinkInfo D2
WHERE D1.type = D2. type
AND D1.drinkId < D2.drinkId
AND D1.type = "soda";
```

#1.20 Try create a table called `publisher`, include `pubid`,`am`,`offer` and `transactionid`, take `pubid` as the primary key.
```{SQL}
CREATE TABLE publisher
('pubid' INTEGER,
'am' TEXT,
'offer' TEXT,
'transactionid' INTEGER,
PRIMARY KEY(pubid));
```

#1.21 Find all the drinkId of cocktail save it as an view
```{SQL}
CREATE VIEW cocktail AS
SELECT *
FROM drinkInfo
WHERE type = "cocktail";
```

# 1.22 Drop the view
```{SQL}
DROP VIEW cocktail;
```
