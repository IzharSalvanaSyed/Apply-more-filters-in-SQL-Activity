# Apply-more-filters-in-SQL-Activity
As a security analyst, querying numbers and dates is crucial. For instance, you might need to filter patch dates to identify machines needing an update or investigate security incidents by filtering login attempts within a specific timeframe. Utilizing common operators for numeric and date data is essential for accurate filtering.


## Table of contents

1. [Scenario](#scenario)
2. [Retrieve login attempts after a certain date](#retrieve)
3. [Retrieve logins in a date range](#range)
4. [Investigate logins at certain times](#investigate)
5. [Investigate logins by event ID](#investigateid)
6. [Conclusion](#conclusion)

## Scenario <a name="scenario">
You need to gather information about login attempts for certain dates and times to resolve a security incident. First, retrieve login events made after a certain date. Then narrow the focus by filtering logins in a date range. Next, investigate logins made at certain times. Finally, filter login attempts based on their event IDs. Time to get started and use operators to filter data from a table!

Common operators for working with numeric or date and time data will help you accurately filter data. These are some of the operators you'll use:

= (equal)
> (greater than)
< (less than)
<> (not equal to)
>= (greater than or equal to)
<= (less than or equal to)

### Note:  
In this task, you need to investigate a recent security incident. To do this, you need to gather information about login attempts made after a certain date.

- Complete the SQL query to retrieve data for login attempts made after `'2022-05-09'`.
`SELECT * FROM log_in_attempts WHERE login_date > '2022-05-09';`

How many login attempts were made after 2022-05-09?

    +----------+----------+------------+------------+---------+-----------------+---------+
    | event_id | username | login_date | login_time | country | ip_address      | success |
    +----------+----------+------------+------------+---------+-----------------+---------+
    |        1 | jrafael  | 2022-05-09 | 04:56:27   | CAN     | 192.168.243.140 |       1 |
    |        2 | apatel   | 2022-05-10 | 20:27:27   | CAN     | 192.168.205.12  |       0 |
    |        3 | dkot     | 2022-05-09 | 06:47:41   | USA     | 192.168.151.162 |       1 |
    |        5 | jrafael  | 2022-05-11 | 03:05:59   | CANADA  | 192.168.86.232  |       0 |
    |        6 | arutley  | 2022-05-12 | 17:00:59   | MEXICO  | 192.168.3.24    |       0 |
    |        7 | eraab    | 2022-05-11 | 01:45:14   | CAN     | 192.168.170.243 |       1 |
    |        9 | yappiah  | 2022-05-11 | 13:47:29   | MEX     | 192.168.59.136  |       1 |
    |       10 | jrafael  | 2022-05-12 | 09:33:19   | CANADA  | 192.168.228.221 |       0 |
    |.....     |          |            |            |         |                 |         |
    +----------+----------+------------+------------+---------+-----------------+---------+
    125 rows in set (0.000 sec)

- 125

Now, based on your first query, you need to expand the date range to include 2022-05-09 in your search.

- Complete the SQL query to retrieve data for login attempts that were made on or after `'2022-05-09'`.
`SELECT * FROM log_in_attempts WHERE login_date >= '2022-05-09';`

How many login attempts were made on or after 2022-05-09?

    +----------+----------+------------+------------+---------+-----------------+---------+
    | event_id | username | login_date | login_time | country | ip_address      | success |
    +----------+----------+------------+------------+---------+-----------------+---------+
    |        1 | jrafael  | 2022-05-09 | 04:56:27   | CAN     | 192.168.243.140 |       1 |
    |        2 | apatel   | 2022-05-10 | 20:27:27   | CAN     | 192.168.205.12  |       0 |
    |        3 | dkot     | 2022-05-09 | 06:47:41   | USA     | 192.168.151.162 |       1 |
    |        5 | jrafael  | 2022-05-11 | 03:05:59   | CANADA  | 192.168.86.232  |       0 |
    |        6 | arutley  | 2022-05-12 | 17:00:59   | MEXICO  | 192.168.3.24    |       0 |
    |        7 | eraab    | 2022-05-11 | 01:45:14   | CAN     | 192.168.170.243 |       1 |
    |        9 | yappiah  | 2022-05-11 | 13:47:29   | MEX     | 192.168.59.136  |       1 |
    |       10 | jrafael  | 2022-05-12 | 09:33:19   | CANADA  | 192.168.228.221 |       0 |
    |.....     |          |            |            |         |                 |         |
    +----------+----------+------------+------------+---------+-----------------+---------+
    165 rows in set (0.000 sec)
    
- 165


## Retrieve logins in a date range <a name="range">
In this task, you need to narrow the focus of the search. Login attempts made after 2022-05-11 shouldn't be included. Use the `BETWEEN` and `AND` operators to return results between `'2022-05-09'` and `'2022-05-11'`.

- Select all the records from the `machines` table with a value of `'OS 2'` in the `operating_system` column.
`SELECT * FROM log_in_attempts WHERE login_date BETWEEN '2022-05-09' AND '2022-05-11';`

Note: The WHERE clause allows you to filter the results returned by a query by returning only the records that satisfy the condition.  

How many login attempts were made between 2022-05-09 and 2022-05-11?

    +----------+----------+------------+------------+---------+-----------------+---------+
    | event_id | username | login_date | login_time | country | ip_address      | success |
    +----------+----------+------------+------------+---------+-----------------+---------+
    |        1 | jrafael  | 2022-05-09 | 04:56:27   | CAN     | 192.168.243.140 |       1 |
    |        2 | apatel   | 2022-05-10 | 20:27:27   | CAN     | 192.168.205.12  |       0 |
    |        3 | dkot     | 2022-05-09 | 06:47:41   | USA     | 192.168.151.162 |       1 |
    |        5 | jrafael  | 2022-05-11 | 03:05:59   | CANADA  | 192.168.86.232  |       0 |
    |        7 | eraab    | 2022-05-11 | 01:45:14   | CAN     | 192.168.170.243 |       1 |
    |        9 | yappiah  | 2022-05-11 | 13:47:29   | MEX     | 192.168.59.136  |       1 |
    |....      |          |            |            |         |                 |         |
    +----------+----------+------------+------------+---------+-----------------+---------+
    123 rows in set (0.055 sec)

- 123       

## Investigate logins at certain times <a name="investigate">
In this task, you need to investigate logins that were made at certain times. To do this, filter the data in the `log_in_attempts` table by login time (`login_time`).

First, your organization's typical work hours begin at 07:00:00. Retrieve all login attempts made before 07:00:00 to learn more about the users who are logging in outside of typical hours.

- Write a SQL query to retrieve data for login attempts made before `'07:00:00'`.
`SELECT * FROM log_in_attempts WHERE login_time < '07:00:00';`

Note: Place time data in single quotation marks.

What is the username of the fifth record returned from this query?
    
    +----------+----------+------------+------------+---------+-----------------+---------+
    | event_id | username | login_date | login_time | country | ip_address      | success |
    +----------+----------+------------+------------+---------+-----------------+---------+
    |        1 | jrafael  | 2022-05-09 | 04:56:27   | CAN     | 192.168.243.140 |       1 |
    |        3 | dkot     | 2022-05-09 | 06:47:41   | USA     | 192.168.151.162 |       1 |
    |        4 | dkot     | 2022-05-08 | 02:00:39   | USA     | 192.168.178.71  |       0 |
    |        5 | jrafael  | 2022-05-11 | 03:05:59   | CANADA  | 192.168.86.232  |       0 |
    |        7 | eraab    | 2022-05-11 | 01:45:14   | CAN     | 192.168.170.243 |       1 |
    |        8 | bisles   | 2022-05-08 | 01:30:17   | US      | 192.168.119.173 |       0 |
    |....      |          |            |            |         |                 |         |
    +----------+----------+------------+------------+---------+-----------------+---------+
    67 rows in set (0.001 sec)

- eraab

The query in the previous step returned more results than required.

- Modify the query to return logins between `'06:00:00'` and `'07:00:00'`.
`SELECT * FROM log_in_attempts WHERE login_time BETWEEN '06:00:00' AND '07:00:00';`

What time was the earliest login attempt between 06:00:00 and 07:00:00?

    +----------+----------+------------+------------+---------+-----------------+---------+
    | event_id | username | login_date | login_time | country | ip_address      | success |
    +----------+----------+------------+------------+---------+-----------------+---------+
    |        3 | dkot     | 2022-05-09 | 06:47:41   | USA     | 192.168.151.162 |       1 |
    |       16 | mcouliba | 2022-05-11 | 06:44:22   | CAN     | 192.168.172.189 |       1 |
    |       24 | arusso   | 2022-05-09 | 06:49:39   | MEXICO  | 192.168.171.192 |       1 |
    |       37 | eraab    | 2022-05-10 | 06:03:41   | CANADA  | 192.168.152.148 |       0 |
    |       71 | mcouliba | 2022-05-09 | 06:57:42   | CAN     | 192.168.55.169  |       0 |
    |       98 | gesparza | 2022-05-11 | 06:30:14   | CANADA  | 192.168.148.80  |       0 |
    |      106 | tmitchel | 2022-05-12 | 06:15:41   | MEXICO  | 192.168.3.252   |       1 |
    |      134 | iuduike  | 2022-05-09 | 06:46:40   | USA     | 192.168.22.115  |       1 |
    |      136 | mabadi   | 2022-05-10 | 06:56:44   | US      | 192.168.214.234 |       1 |
    |      142 | gesparza | 2022-05-11 | 06:31:14   | CANADA  | 192.168.117.56  |       1 |
    |      147 | yappiah  | 2022-05-08 | 06:04:34   | MEX     | 192.168.65.245  |       0 |
    |      148 | daquino  | 2022-05-08 | 06:15:55   | CANADA  | 192.168.135.6   |       1 |
    |      182 | lyamamot | 2022-05-10 | 06:01:31   | USA     | 192.168.106.52  |       0 |
    |      191 | cjackson | 2022-05-08 | 06:46:07   | CANADA  | 192.168.7.187   |       0 |
    |      195 | alevitsk | 2022-05-11 | 06:59:13   | CANADA  | 192.168.236.78  |       1 |
    +----------+----------+------------+------------+---------+-----------------+---------+
    15 rows in set (0.001 sec)
    
- 33

## Investigate logins by event ID <a name="investigateid">
In this task, you need to investigate login attempts based on event ID numbers. With this query, you want to return only the event_id, username, and login_date fields from the log_in_attempts table.

Note: The `event_id` column contains numeric data; do not place numeric data in quotation marks.  

- Write a query to return login attempts with `event_id` greater than or equal to 100.
`SELECT * FROM log_in_attempts WHERE event_id >= '100';`

What is the login date of the third result returned by your query?

    +----------+----------+------------+------------+---------+-----------------+---------+
    | event_id | username | login_date | login_time | country | ip_address      | success |
    +----------+----------+------------+------------+---------+-----------------+---------+
    |      100 | tmitchel | 2022-05-12 | 16:02:03   | MEXICO  | 192.168.97.225  |       0 |
    |      101 | sbaelish | 2022-05-08 | 12:01:22   | US      | 192.168.145.158 |       0 |
    |      102 | jreckley | 2022-05-09 | 16:51:44   | MEX     | 192.168.108.13  |       1 |
    |      103 | jhill    | 2022-05-11 | 09:10:54   | US      | 192.168.60.153  |       0 |
    |      104 | asundara | 2022-05-11 | 18:38:07   | US      | 192.168.96.200  |       0 |
    |....      |          |            |            |         |                 |         |
    +----------+----------+------------+------------+---------+-----------------+---------+
    101 rows in set (0.092 sec)
    
- 2022-05-09

The query in the previous step returned more data than required.

Modify the query to return only login attempts with `event_id` between `100` and `150`.
`SELECT * FROM log_in_attempts WHERE event_id BETWEEN '100' AND '150';`

What is the username of the seventh result returned by your query?

    +----------+----------+------------+------------+---------+-----------------+---------+
    | event_id | username | login_date | login_time | country | ip_address      | success |
    +----------+----------+------------+------------+---------+-----------------+---------+
    |      100 | tmitchel | 2022-05-12 | 16:02:03   | MEXICO  | 192.168.97.225  |       0 |
    |      101 | sbaelish | 2022-05-08 | 12:01:22   | US      | 192.168.145.158 |       0 |
    |      102 | jreckley | 2022-05-09 | 16:51:44   | MEX     | 192.168.108.13  |       1 |
    |      103 | jhill    | 2022-05-11 | 09:10:54   | US      | 192.168.60.153  |       0 |
    |      104 | asundara | 2022-05-11 | 18:38:07   | US      | 192.168.96.200  |       0 |
    |      105 | cjackson | 2022-05-12 | 19:36:42   | CAN     | 192.168.247.153 |       1 |
    |      106 | tmitchel | 2022-05-12 | 06:15:41   | MEXICO  | 192.168.3.252   |       1 |
    |      107 | bisles   | 2022-05-12 | 20:25:57   | USA     | 192.168.116.187 |       0 |
    |      108 | daquino  | 2022-05-09 | 21:30:48   | CANADA  | 192.168.15.110  |       1 |
    |....      |          |            |            |         |                 |         |
    +----------+----------+------------+------------+---------+-----------------+---------+
    51 rows in set (0.001 sec
    
- tmitchel

## Conclusion <a name="conclusion">:
We now have practical experience in using SQL to filter for numbers and dates to extract all sorts of useful data by using:

- the WHERE keyword
- the BETWEEN and AND operators, and
- operators for working with numeric or date and time data types (for example, =, >, >=)
