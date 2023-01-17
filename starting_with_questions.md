Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

SELECT city, country, transactions, totaltransactionrevenue
	FROM all_sessions
		WHERE transactions IS NOT NULL
		ORDER BY transactionrevenue DESC
		LIMIT 1
	


Answer:

Palo Alto, USA


**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

SELECT country, city, ROUND(AVG(productquantity),2) AS average_ordered, fullvisitorid
	FROM all_sessions
		WHERE productquantity IS NOT NULL
		GROUP BY country, city, productquantity, fullvisitorid
		ORDER BY productquantity DESC

Answer:

The preceeding code will list of countries, cities and average products purchased.



**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

 SELECT country, city, v2productcategory
	FROM all_sessions
	WHERE city <> 'not available in demo dataset' AND city <> '(not set)'
	GROUP BY country, city, v2productcategory
	ORDER BY country, city, v2productcategory

Answer:

There are a few patterns you can see from the data. For instance in Sydney, Australia there are a lot of orders being made and many of them are for apparel for people of all ages.


**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

SELECT country, city, v2productname, MAX(productquantity) AS prod
	FROM all_sessions
	WHERE city <> 'not available in demo dataset' AND city <> '(not set)'
		AND productquantity IS NOT NULL
	GROUP BY country, city, v2productname
	ORDER BY prod DESC
	
Answer:

Few cities have a product that they sell more of than others with a few exceptions: Salem USA sells more Red Spiral Google Notebooks, and Waze Dress Socks sell better in Madrid Spain than anything else. 
Another thing to note might be that more variety of sales are made in areas like Mountain View, USA and New York USA.



**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

SELECT SUM(revenue) 
	FROM analytics

SELECT alls.country, alls.city, SUM(ant.revenue) total_revenue
	FROM all_sessions AS alls
	INNER JOIN analytics AS ant
	 	ON alls.visitid = ant.visitid
		WHERE city <> 'not available in demo dataset' AND city <> '(not set)'
		AND ant.revenue IS NOT NULL
	GROUP BY alls.country, alls.city
	ORDER BY total_revenue DESC

Answer:



We can see that most of the revenue is generated in the USA, and that New York USA generates more revenue than the next two highest grossing cities (Sunnyvale and Mountain View USA) combined.
We can also see that revenue generated outside of the USA counts for less than a one hundreth of a percent of the total revenue.



