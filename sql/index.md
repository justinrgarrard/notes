---
layout: page
---

### SQL Exercises (Postgresql)

https://pgexercises.com

* [Basics](basics.md)
* [Joins](joins.md)
* [Modify Data](modify_data.md)
* [Aggregation](aggregation.md)

### Use the Index Luke

https://use-the-index-luke.com/

* [High Level Notes](use_the_index_luke.md)

---

### Helpful Vocabulary

**Common Table Expression (CTE)**: `with <table> as...` 

Create a database view inside a query. Similar to a subquery. Helpful for improving readability of complex queries with redundant code.

```sql
with sum as (select facid, sum(slots) as totalslots
	from cd.bookings
	group by facid
)
select facid, totalslots 
	from sum
	where totalslots = (select max(totalslots) from sum);
```

**Grouping Sets**: `rollup(), cube()`

Creates a hierarchy of aggregations. For example, `rollup(facid, month)` produces a table that contains:

* (facid, month)
* (month)
* () 

| facid | month | slots |
| ----- | ----- | ----- |
| 0     | 9     | 21    |
| 0     | 10    | 36    |
| 0     |       | 57    |

`cube(facid, month)` would produce all possible combinations.

* (facid, month)
* (month)
* (facid)
* () 


