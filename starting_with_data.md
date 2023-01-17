Question 1: What percentage of people who visited the web site made a purchase?

SQL Queries:

SELECT COUNT(fullvisitorid)
	FROM all_sessions

SELECT COUNT(transactions)
	FROM all_sessions

Answer: 
With 15,134 visits and only 81 transactions made, only 0.0066% of people who visited the web site made a purchase.


Question 2: Are people who spend more time on the website more likely to buy products than those who look only briefly?

SQL Queries:

SELECT country, city, timeonsite, totaltransactionrevenue, productquantity
	FROM all_sessions
		WHERE productquantity IS NOT NULL

Answer:

From this query we can see that not many purchases have been made from the given the data. We can also see that purchases have been made from as little time as 83 seconds, and as much time as 1147 seconds and with quite a range in between. I would say that time spent on site is not a reliable factor.



Question 3: What countries would you find the highest number of people looking for products? 

SQL Queries:

SELECT country, COUNT(pageviews) AS site_visits
	FROM  all_sessions
		WHERE country <> 'not available in demo dataset' AND country <> '(not set)'
		GROUP BY country
		ORDER BY site_visits DESC

Answer:

The data is certainly skewed with the USA clearly showing a higher number of visits to the web sites than other countries.