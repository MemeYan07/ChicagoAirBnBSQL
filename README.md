# ChicagoAirBnBSQL

--Clean Data by removing the dollar signs and converting it into an integer data type
SELECT * FROM;
REPLACE(price, '$', '') AS UNSIGNED; “image”

--selects specific columns, while calculating Projected Revenue
SELECT id,listing_url, name, neighbourhood, neighbourhood_cleansed, price, 30 - availability_30 AS Bookings_30,
price * (30 - availability_30) AS Projected_Revenue
FROM Airbnb

--Organizing the preferred dataset I’d like to analyze
SELECT id,host_name, neighbourhood_cleansed, availability_365, price AS PricePerNight , 30 - availability_30 AS Bookings_30,
price * (30 - availability_30) AS Projected_Revenue
FROM Airbnb
ORDER BY Projected_Revenue DESC
LIMIT 20;

--removing 0 availability for the year with the WHERE statement to provide a more accurate dataset
SELECT id,host_name, neighbourhood_cleansed, availability_365, price AS PricePerNight , 30 - availability_30 AS Bookings_30,
price * (30 - availability_30) AS Projected_Revenue
FROM Airbnb
WHERE availability_365 > 0
ORDER BY Projected_Revenue DESC
LIMIT 20;

--retrieves the count of listings in each unique 'neighbourhood_cleansed' from the 'Airbnb' table
SELECT neighbourhood_cleansed, COUNT(*) AS ListingCount
FROM Airbnb
GROUP BY neighbourhood_cleansed
ORDER BY ListingCount DESC
LIMIT 10;

--selects specific columns (id, host_name, etc.) from the 'Airbnb' table, calculates the difference between 30 and 'availability_30' as 'Bookings_30,' and computes projected revenue for listings with availability greater than 0 days in the 'Airbnb' table, grouping results by neighborhood, and then displaying the top 10 neighborhoods with the highest projected revenue, ordered in descending order.

SELECT id,host_name, neighbourhood_cleansed AS Neighborhood, price AS PricePerNight, 30 - availability_30 AS Bookings_30,
price * (30 - availability_30) AS Projected_Revenue
FROM Airbnb
WHERE availability_365 > 0
GROUP BY neighbourhood_cleansed
ORDER BY Projected_Revenue DESC
LIMIT 10;

--calculates the count of listings, bookings, and projected revenue for hosts in each neighborhood from the 'Airbnb' table where availability for the year is greater than 0, grouping results by both neighborhood and host, and then orders them by the count of listings and projected revenue in descending order.
SELECT neighbourhood_cleansed AS Neighborhood, host_id,COUNT(*) AS ListingCount, 30 - availability_30 AS Bookings_30,
price * (30 - availability_30) AS Projected_Revenue
FROM Airbnb
WHERE availability_365 > 0
GROUP BY neighbourhood_cleansed, host_id
ORDER BY ListingCount DESC, Projected_Revenue DESC;

--comprehensive count of sanitation-related complaints.
SELECT COUNT(*) AS total_complaints
FROM (
SELECT comments
FROM review
WHERE (comments) LIKE '%dirty%' OR (comments) LIKE '%unclean%' OR (comments) LIKE '%sanitation%');

--retrieves data from the 'Review' table, specifically the columns listed, for reviews containing keywords like 'dirty,' 'unclean,' or 'sanitation,'
SELECT listing_id, id, reviewer_name, reviewer_id, comments
FROM Review
WHERE (comments) LIKE '%dirty%' OR (comments) LIKE '%unclean%' OR (comments) LIKE '%sanitation%'
ORDER BY listing_id ASC, id ASC;

--Finding coinciding data column between the AirBnB dataset and the Review dataset
SELECT listing_id, id
FROM Review
GROUP BY listing_id
ORDER BY listing_id ASC;
SELECT *
FROM Airbnb
ORDER BY id ASC, host_id ASC;

--The coinciding id, host_name, and host_id to contact potential clients for cleaning business from the Airbnb table based on negative sanitation-related complaints
SELECT listing_id, id, reviewer_name, reviewer_id, comments
FROM Review
WHERE (comments) LIKE '%dirty%' OR (comments) LIKE '%unclean%' OR (comments) LIKE '%sanitation%'
ORDER BY listing_id ASC, id ASC;

SELECT ID, Host_name, HOST_ID
FROM Airbnb
GROUP BY ID
ORDER BY ID ASC, host_ID ASC; 
