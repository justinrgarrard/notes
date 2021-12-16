---
layout: page
---

-- Aggregation

![Schema Vis](schema-horizontal.svg)

***Count***

```sql
-- Count
select
	count(*) as count
from
	cd.facilities;
```

```sql
-- Count + Projection
select
    facid, 
	(select count(*) from cd.facilities)
from 
    cd.facilities;
```

```sql
-- Count Unique Values
select
	count(distinct address) as unique_addresses
from
	cd.facilities;
```

```sql
select
	recommendedby,
	count(*)
from
	cd.members
where
	recommendedby is not null
group by 
	recommendedby
order by
	recommendedby;
```

***Sum***

```sql
select
	facid,
	sum(slots) as "Total Slots"
from
	cd.bookings
where
	starttime >= '2012-09-01' and
	starttime < '2012-10-01'
group by
	facid
order by
	sum(slots);
```

```sql
-- Non-optimized Date Query w/ Aggregation
select
	facid,
	extract(month from starttime) as month,
	sum(slots) as "Total Slots"
from
	cd.bookings
where
	extract(year from starttime) = 2012
group by
	facid, month
order by
	facid, month;
```

```sql
-- Optimized for Index Query w/ Aggregation
select
    facid,
    extract(month from starttime) as month,
    sum(slots) as "Total Slots"
from 
    cd.bookings
where
    starttime >= '2012-01-01'
    and starttime < '2013-01-01'
group by
    facid, month
order by
    facid, month;
```

```sql
-- Demo of the HAVING clause
---- WHERE filters inputs
---- HAVING filters outputs
select
	facid,
	sum(slots) as "Total Slots"
from
	cd.bookings
group by
	facid
having
	sum(slots) > 1000
order by
	facid;
```

```sql
-- When HAVING fails
---- PostgreSQL does not recognize column names in HAVING
---- Hence, we use a subquery here
select
	name, revenue from (
	  select
		  facilities.name,
		  sum(
			  case when bookings.memid = 0 then
				  facilities.guestcost
			  else
				  facilities.membercost
			  end * slots) as revenue
	  from
		  cd.facilities
		  inner join cd.bookings on facilities.facid = bookings.facid
	  group by
		  facilities.name) as agg
where
	revenue < 1000
order by
	revenue;
```

***Min***

```sql
-- Find first date of booking after 2012-09-01
select
	members.surname,
	members.firstname,
	members.memid,
	min(bookings.starttime)
from
	cd.members
	inner join cd.bookings on members.memid = bookings.memid
where
	bookings.starttime > '2012-09-01'
group by 
	members.surname,
	members.firstname,
	members.memid
order by
	members.memid;
```

***Misc***

```sql
-- Using ROLLUP
---- ROLLUP is a PostgreSQL special
---- Mimics numerous UNION ALL statements
select
	bookings.facid,
	extract(month from bookings.starttime) as month,
	sum(bookings.slots) as slots
from
	cd.bookings
where
	starttime >= '2012-01-01' and
	starttime < '2013-01-01'
group by
	rollup(bookings.facid, month)
order by
	bookings.facid, month
```

```sql
-- Strings and Rounding
select
	bookings.facid,
	facilities.name,
	trim(to_char(sum(slots) / 2.0, '9999999999999999D99')) as "Total Hours" 
from
	cd.bookings
	inner join cd.facilities on bookings.facid = facilities.facid
group by
	bookings.facid,
	facilities.name
order by
	facid;
```

```sql
-- Toy Windowing Example
---- Replaces a subquery
select count(*) over(), firstname, surname
	from cd.members
order by joindate 
```