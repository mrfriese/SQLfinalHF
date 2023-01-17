What issues will you address by cleaning the data?

(1) Removal of some categories with NULL, or calculate values from applicable columns.

(2) Divide unit cost by 1,000,000.

(3) Rename time columns to time in seconds

(3) Remove redundant columns like ecommercereaction_type and ecommercereaction_step.

(4) Remove duplicate Ids in the data.

Queries:
Below, provide the SQL queries you used to clean your data.

(1) ALTER TABLE all_sessions
        DROP column type

    * Note: There are other tables that are mostly filled with NULL values that I have chosen to keep as some of the values serve a purpose.

(2) SELECT unit_price/1000000 AS price_of_unit
	FROM analytics

(3) SELECT time AS time_in_seconds
        FROM all_sessions

(4) SELECT DISTINCT fullvisitorid, *
    FROM all_sessions
    ORDER BY fullvisitorid
    

