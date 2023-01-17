What are your risk areas? Identify and describe them.

- Lots on missing data. The majority of the values that we are using to calculate our queries of interest have not data inputed. This problem can cause the results of one query to not match the results of another, which might make the company using the data to make the wrong decision.

- Unit values: If unit values like unit price, or quantity sold are not formatted to mean the same thing, then the data might become skewed to show that more of one thing is sold in one area when really that isn't the case.

- Duplicate IDs: Again this will skew the data. Multilple entries of the same data will create a false total when working off of and cause the data to lean in one direction which has the potential to cause a costly business decision.


QA Process:
Describe your QA process and include the SQL queries used to execute it.

To begin with I looked at the fullvisitorids to verify that there are only unique entries listed:

SELECT COUNT(DISTINCT(visitId))
	FROM all_sessions

returns 15134

SELECT COUNT(visitid)
	FROM all_sessions

returns 15134

These numbers match, so I can continue my cleaning knowing that there are not duplicates visits.
If I had used 'fullvisitorid' for the same query I would have gotten a difference in results. That shows that there have been users who have visited the web site more than once, but it is useful to note the difference.


Looking at units it is not clear if all the data inputted is in the same format (unlikely I would guess), so it is difficult to proceed by basing queries on categories that have potentially inconsistent values. In the assignment we were asked to divide the unit cost by 1,000,000:

SELECT (unit_price/1000000)
	FROM analytics

This makes the data make a little more sense, but this isn't some thing that we can use across the board. For example:

SELECT productprice
	FROM all_sessions
	LIMIT 30 

Some of the data here have values less than 1,000,000. If we were to use the same cleaning step it may effectively eliminate use of that data point from any further queries.


Missing data. This is probably my biggest concern that I have discussed so far. There is incredibly substancial amount of data missing here. Most of the recorded transactions do not reflect the revenue that this company has made, and the data it does show localizes any profitable areas in the USA and ignores the rest of the cities and countries that business is being performed in.
Most of the web searches are more spread out to areas outside the USA, but that information is not reflected in the revenue that the company makes.

I have used a few queries to minimize the data I am looking at to entries that have more information filled in:

SELECT *
	FROM all_sessions
		WHERE city <> 'not available in demo dataset' AND city <> '(not set)'

The above query eliminates the entries where city data is not entered.

total_revenue
	FROM all_sessions AS alls
	INNER JOIN analytics AS ant
	 	ON alls.visitid = ant.visitid
		WHERE city <> 'not available in demo dataset' AND city <> '(not set)'
		AND ant.revenue IS NOT NULL
	GROUP BY alls.country, alls.city
	ORDER BY total_revenue DESC

The query above I used to answer question 5 in starting_with_questions. In the table 'analytics' I set another condition where transactions without revenue were elimiated so avoid showing business in areas that not data had been recorded.
