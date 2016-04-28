---
inFeed: true
hasPage: true
inNav: true
inLanguage: null
keywords: []
description: "This Oracle SQL tutorial started as a list of SQL tuning tips but that's of limited use on its own so we've expanded the tips to explain how and why they work to make this a more complete Oracle SQL tutorial."
datePublished: '2016-04-28T11:17:27.210Z'
dateModified: '2016-04-28T11:17:26.707Z'
title: Oracle SQL Tutorial - A Few Hints And Tips On How To Optimize Your SQL
author: []
authors: []
publisher:
  name: null
  domain: null
  url: null
  favicon: null
starred: false
sourcePath: _posts/2016-04-28-oracle-sql-tutorial-a-few-hints-and-tips-on-how-to-optimiz.md
published: true
url: oracle-sql-tutorial-a-few-hints-and-tips-on-how-to-optimiz/index.html
_type: Article

---
# Oracle SQL Tutorial - A Few Hints And Tips On How To Optimize Your SQL

This Oracle SQL tutorial started as a list of SQL tuning tips but that's of limited use on its own so we've expanded the tips to explain how and why they work to make this a more complete Oracle SQL tutorial.

Before we start, there is one important principle regarding Oracle that is important to remember when writing SQL and that is that Oracle caches the **compiled **SQL and is therefore able to reuse statements which are **exactly**the same as previously executed statements. 

To take advantage of this feature the SQL has to be exactly the same - including case, number of spaces, new lines etc. and has to refer to the same objects (so if you had the same table in different schemas and ran the query as different users, it would have to be re-parsed because it would not be able to use the same object).

What's the benefit of being able to reuse queries? This saves the time and resources required to parse the statement and determine the execution plan thereby making your Oracle database much more efficient, able to handle greater loads and enabling your applications to scale to support more users.

Let's get started with this Oracle SQL tutorial.

## _Use Views_

One way to ensure that queries are the same is to use views. Views are merely predefined queries. The source code of all views (i.e. the SQL on which they are based) is stored in the database in the data dictionary. This means that by using views in all your programs, by definition you are using exactly the same queries every time and therefore eliminating the re-parsing overhead.

## Materialized Views

In Oracle 8i and above there is a special type of view called a

materialized view.

This takes the concept of a view one stage further: - instead of just storing the SQL statement underlying the view, the results of the query are stored, hence the view is said to be materialized. This doesn't just eliminate the relatively small parsing overhead it eliminates completely the overhead from running the query as well.

## _Oracle Tips & Tricks to SKYROCKET Your Career!_

If you're not already a subscriber to Oracle Tips and Tricks, you're missing out on a myriad of tips and techniques to help you become a better, faster, smarter developer. **[Subscribe now][0]**and ignite your career.

Materialized views are commonly used in data warehouses where information (e.g. sales data) is required at various levels and by various dimensions (e.g. by time: week, month, quarter, year to date etc.; by organization hierarchy: sales team, area, country, region) where it would take a long while and be wasteful to run the query every time somebody wanted it.

The advantage of using materialized views is that they can be managed completely by the database, being refreshed automatically when any of the underlying tables change or on pre-defined schedule and they can be used without having to change a line of code. This is because the optimizer in Oracle will automatically rewrite a query to use a materialized view if it will improve performance (as long as the QUERY\_REWRITE\_ENABLED initialization parameter is set). See the [Oracle Database Concepts][1] manual for more details.

### Object Views

Although not strictly useful for improving performance (which is the main subject of this Oracle SQL tutorial), it is worth noting that in Oracle8 and above is another type of view called object views which are used to wrap relational-database tables into an object-oriented database object so that languages like Java can manipulate them more easily.

The use of this type of view would not probably not help run-time performance - they are more useful for application developers to avoid having to map objects onto relational data. One potential disadvantage of object views is that they can only be updated via

instead-of

triggers (which fire instead of normal update, delete or insert operations - hence the name) or via direct calls to PL/SQL procedures.

The next part of this Oracle SQL tutorial looks at how you can use PL/SQL to improve performance.[Oracle SQL tutorial part 2: using stored procedures][2]

[Part3][3] examines why you should use bind variables in your queries.

[Part 4 of this Oracle SQL tutorial][4] examines why you should use only selective indexes in your queries.

[Part 5][5] explains why sometimes you should **not **use an index in your queries

[Part 6][6] explains how to optimise join queries for peak performance.

[Part 7][7] explains why it is better to name the columns in your SQL queries.

To learn more about Oracle, see our [Oracle training][8] page for information about formal training either on-line or classroom-based.

For SQL tips for SQL Server database see [SQL Server Pro][9]

[Business Analysis-The REAL WORLD][10] presents eBooks on Business Analysis, based on real world experiences, covering specific topics of documenting business processes and literally walks a Business Analyst through each step of an IT project to gather and document business requirements.

[0]: http://www.asktheoracle.net/oracle-tips-signup.html
[1]: http://docs.oracle.com/cd/E16655_01/server.121/e17633/schemaob.htm#CNCPT411
[2]: http://www.asktheoracle.net/oracle-sql-tutorial-part2.html
[3]: http://www.asktheoracle.net/oracle-sql-tutorial-part3.html
[4]: http://www.asktheoracle.net/oracle-sql-tutorial-part4.html
[5]: http://www.asktheoracle.net/oracle-sql-tutorial-part5.html
[6]: http://www.asktheoracle.net/oracle-sql-tutorial-part6.html
[7]: http://www.asktheoracle.net/oracle-sql-tutorial-part7.html
[8]: http://www.asktheoracle.net/oracle-training.html
[9]: http://www.sql-server-pro.com/learn-sql.html
[10]: http://www.businessanalysis-therealworld.com/