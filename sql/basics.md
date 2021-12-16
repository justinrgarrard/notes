---
layout: page
---

# SQL Basics

![Schema Vis](schema-horizontal.svg)

***Selection and Ordering***

```sql
# Query everything in a table
select
	*
from
	cd.facilities;
```

```sql
# Query by Column
select
	name,
	membercost
from
	cd.facilities;
```

```sql
# Query with Qualifiers
select
	*
from
	cd.facilities
where 
	membercost > 0;
```

```sql
# Query with Calculations
select
	facid,
	name,
	membercost,
	monthlymaintenance
from
	cd.facilities
where
	membercost > 0 and
	membercost < (monthlymaintenance / 50);
```

```sql
# Query with Dates
select 
	memid,
	surname,
	firstname,
	joindate
from
	cd.members
where
	joindate >= '2012-09-01';
```

```sql
# Query with Aggregation
select
	max(joindate) as latest
from
	cd.members;
```

```sql
# Find latest join date and member info
select
	firstname,
	surname,
	joindate
from
	cd.members
where joindate = (
		select max(joindate) from cd.members
	); 
```

***Search and Pattern Matching***

```sql
# Standard
select
	*
from
	cd.facilities
where
	name like '%Tennis%';
```

```sql
# Regex
select
	*
from
	cd.facilities
where
	name ~ '.*Tennis.*';
```

```sql
# Hard-coded Expected Response
select
	*
from
	cd.facilities
where
	facid in (1, 5);
```

```sql
# Subquery Expected Response (Toy Example)
select
	* 
from
	cd.facilities
where
	facid in (
		select facid from cd.facilities
	);
```

***Switch Case***

```sql
# Create new column "cost" using case statement
select
	name, 
	case when (monthlymaintenance > 100) then
		'expensive'
	else
		'cheap'
	end as cost
from
	cd.facilities;   
```

***Combine Tables (By Row)***

```sql
select surname 
	from cd.members
union
select name
	from cd.facilities;   
```

***Combine Tables (By Column)***

```sql
select distinct
	recs.firstname as firstname,
	recs.surname as surname
from 
	cd.members mems
	inner join cd.members recs on recs.memid = mems.recommendedby
order by
	surname, firstname;  
```