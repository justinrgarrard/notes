---
layout: page
---

# SQL Joins

![Schema Vis](schema-horizontal.svg)


***Simple Inner Joins***

```sql
-- Inner Join
select
	bookings.starttime
from
	cd.bookings
	inner join cd.members on bookings.memid = members.memid
where
	members.firstname = 'David' and
	members.surname = 'Farrell';
```

```sql
-- Same Inner Join, Different Syntax
select 
	bookings.starttime
from
	cd.bookings,
	cd.members
where
	members.firstname='David' and
	members.surname='Farrell' and
	members.memid = bookings.memid;
```

```sql
-- Inner Join w/ Additional Filtering
select
	bookings.starttime as start,
	facilities.name as name
from
	cd.bookings
	inner join cd.facilities on bookings.facid = facilities.facid
where
	facilities.name ~ '.*Tennis Court.*' and
	bookings.starttime >= '2012-09-21' and
	bookings.starttime < '2012-09-22'
order by bookings.starttime;
```

***Fancy Inner Joins***

```sql
-- Inner Join to the Same Table
-- Requires aliases
select distinct
	recs.firstname as firstname,
	recs.surname as surname
from 
	cd.members mems
	inner join cd.members recs on recs.memid = mems.recommendedby
order by
	surname, firstname;  
```

```sql
-- Double Inner Join
select distinct
	members.firstname || ' ' || members.surname as member,
	facilities.name as facility
from 
	cd.members
	inner join cd.bookings on members.memid = bookings.memid
	inner join cd.facilities on bookings.facid = facilities.facid
where
	facilities.name ~ '.*Tennis Court.*'
order by
	member, facility;
```

```sql
-- Double Inner Join w/ Switch Case
-- Notice that we cannot reference cost in the where clause
select
	members.firstname || ' ' ||  members.surname as member,
	facilities.name,
	case
		when bookings.memid = 0 then
			(facilities.guestcost * bookings.slots)
		else
			(facilities.membercost * bookings.slots) 
	end as cost
from
	cd.members
	inner join cd.bookings on members.memid = bookings.memid
	inner join cd.facilities on bookings.facid = facilities.facid
where
	starttime >= '2012-09-14' and
	starttime < '2012-09-15' and
	(
		(members.memid = 0 and bookings.slots*facilities.guestcost > 30) or
		(members.memid != 0 and bookings.slots*facilities.membercost > 30)
	)
order by 
	cost desc;
```

***Outer Joins***

```sql
-- Combine "members" with itself, presenting recommenders if
-- they exist or Null otherwise
select
	mems.firstname as memfname,
	mems.surname as memsname,
	recs.firstname as recfname,
	recs.surname as recsname
from
	cd.members mems
	left outer join cd.members recs on recs.memid = mems.recommendedby
order by
	memsname, memfname; 
```

***Subqueries***

```sql
-- "Inner Join" but as a Subquery
select distinct
	members.firstname,
	members.surname
from 
	cd.members
where 
	members.memid in (
		select members.recommendedby from cd.members
	)
order by
	surname, firstname;
```

```sql
-- "Outer Join" but as a subquery
select distinct
	members.firstname || ' ' || members.surname as member,
	(select
	 	mems.firstname || ' ' || mems.surname
	 from
	 	cd.members mems
	 where
	 	mems.memid = members.recommendedby) as recommender
from
	cd.members
order by
	member;     
```

```sql
-- Using subqueries to reference columns in the where clause
select
	member,
	facility,
	cost
from 
	(select
	 	members.firstname || ' ' || members.surname as member,
		facilities.name as facility,
	 	case
	 		when members.memid = 0 then
	 			bookings.slots * facilities.guestcost
	 		else
	 			bookings.slots * facilities.membercost
	 	end as cost
	 from
		cd.members
		inner join cd.bookings on members.memid = bookings.memid
		inner join cd.facilities on bookings.facid = facilities.facid
	 where
	 	bookings.starttime >= '2012-09-14' and
	 	bookings.starttime < '2012-09-15'
	 ) as bookings
where
	cost > 30
order by
	cost desc;
```