What issues will you address by cleaning the data?

(1) Removal of categories with NULL, or calculate values from applicable columns.

(2) Divide unit cost by 1,000,000.

(3) Set time in seconds to minutes

(3) Remove redundant columns like ecommercereaction_type and ecommercereaction_step.

(4) Remove duplicate Ids in the data.

Queries:
Below, provide the SQL queries you used to clean your data.

(2)

(4) SELECT DISTINCT fullvisitorid, *
FROM all_sessions
ORDER BY fullvisitorid
LIMIT 20

