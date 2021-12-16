---
layout: page
---

# Modify Data

![Schema Vis](schema-horizontal.svg)

***Insertion***

```sql
-- Insertion
insert
    into cd.facilities
	    (facid, name, membercost, guestcost, initialoutlay, monthlymaintenance)
	values 
        (9,'Spa',20,30,100000,800),
        (10, 'Squash Court 2', 3.5, 17.5, 5000, 80);
```

```sql
-- Manual Dynamic ID
insert
	into cd.facilities
		(facid, name, membercost, guestcost, initialoutlay, monthlymaintenance)
	values
		(select max(facid from cd.facilities)+1, 'Spa', 20, 30, 100000, 800)
```

***Updates***

```sql
-- Update
update
	cd.facilities
set
	membercost = 6,
	guestcost = 30
where
	name ~ '.*Tennis Court.*';
```

```sql
-- Update Using Selection
update
	cd.facilities
set
	membercost = (
        select
            membercost * 1.1
        from
            cd.facilities
        where
            facid = 0),
	guestcost = (
        select 
            guestcost * 1.1 
        from 
            cd.facilities 
        where
            facid = 0)
from facilities
where
	facilities.facid = 1;
```

```sql
-- Update Using Selection
-- PostgreSQL Exclusive (non-standard)
update
	cd.facilities
set
	membercost = facs2.membercost * 1.1,
	guestcost = facs2.guestcost * 1.1
from
	(select
	 	*
	 from
	 	cd.facilities
	 where
	 	facid = 0
	 ) facs2
where
	facilities.facid = 1;
```

***Deletion***

```sql
-- Deletion
delete from
	cd.members
where
	members.memid = 37;
```

```sql
-- Deletion w/ Subquery
delete from
	cd.members
where
	memid not in (
	  select
	  	memid
	  from
	  	cd.bookings
	  );
```
