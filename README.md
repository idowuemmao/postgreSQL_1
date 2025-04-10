##SQL Practice – Club Database Queries

This document contains a collection of beginner to intermediate-level SQL queries written to solve various data retrieval tasks on a sample `cd` (Club Database) schema. 
These queries are helpful for those looking to improve their SQL skills, especially with real-world style questions.
---
1. Retrieve all the information from the cd.facilities table
SELECT * FROM cd.facilities;
2. Retrieve a list of all facility names and their cost to members
SELECT name, membercost FROM cd.facilities;
3. List all facilities that charge a fee to members
SELECT * FROM cd.facilities
WHERE membercost > 0;
4. Facilities charging a fee to members, where the fee is less than 1/50th of the monthly maintenance cost
SELECT facid, name, membercost, monthlymaintenance FROM cd.facilities
WHERE membercost > 0 
AND (membercost < monthlymaintenance / 50);
5. List all facilities with the word 'Tennis' in their name
SELECT * FROM cd.facilities 
WHERE name LIKE '%Tennis%';
6. Retrieve details of facilities with ID 1 and 5 (without using OR)
SELECT * FROM cd.facilities 
WHERE facid IN (1, 5);
7. List members who joined after September 1, 2012
SELECT memid, surname, firstname, joindate 
FROM cd.members 
WHERE joindate > '2012-09-01';
8. Ordered list of the first 10 distinct surnames in the members table
SELECT DISTINCT surname 
FROM cd.members 
ORDER BY surname 
LIMIT 10;
9. Get the signup date of the last member
SELECT joindate 
FROM cd.members 
ORDER BY joindate DESC 
LIMIT 1;
10. Count of facilities with a guest cost of 10 or more
SELECT COUNT(*) 
FROM cd.facilities 
WHERE guestcost > 10;
11. Total number of slots booked per facility in September 2012
SELECT facid, SUM(slots) AS TotalSlots 
FROM cd.bookings 
WHERE starttime >= '2012-09-01' AND starttime < '2012-10-01'
GROUP BY facid
ORDER BY TotalSlots;
12. Facilities with more than 1000 slots booked (sorted by facility ID)
SELECT facid, SUM(slots) AS TotalSlots 
FROM cd.bookings 
GROUP BY facid
HAVING SUM(slots) > 1000
ORDER BY facid;
13. Start times for bookings of tennis courts on '2012-09-21'
SELECT starttime, name 
FROM cd.bookings 
INNER JOIN cd.facilities 
ON cd.facilities.facid = cd.bookings.facid
WHERE name LIKE '%Tennis Court%' 
AND starttime >= '2012-09-21' 
AND starttime < '2012-09-22' 
ORDER BY starttime;
14. Start times for bookings by members named 'David Farrell'
SELECT starttime 
FROM cd.bookings 
LEFT JOIN cd.members 
ON cd.members.memid = cd.bookings.memid
WHERE surname = 'Farrell' 
AND firstname = 'David';

