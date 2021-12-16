---
layout: page
---

# Use the Index Luke Draft Notes

### Preface

* SQL describes **what** the system is doing, not **how** the system does it


* An index is a constantly shifting directory of where data is stored in a database
  * An index takes up space
  * An index must be kept up-to-date


* Under the hood, an index is stored as a doubly-linked list tied to a B-Tree
  * The B-Tree serves as a pseudo-hashmap; it holds references to each node in a hierarchical structure
  * The doubly-linked list holds the acutal index, with each node referencing database table data


* Rebuilding an index is not generally a helpful action when troubleshooting slow lookups


### The Where Clause

* Using `where` on an indexed column allows you to skip the B-Tree, speeding up query times

* Tables that use **concatenated indexes** should be queried using all required indexes
  * Order is important when doing so
  * Particularly helpful when planning for queries that are almost always done using multiple columns (i.e. firstname/lastname)

* **Access Paths** are the most commonly used queries for a given databasse
  * These are generally only known by the users/developers on a database
  * Maybe there's a command for DBA's to find this info?
