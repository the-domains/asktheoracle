---
inFeed: false
hasPage: true
inNav: true
inLanguage: null
keywords: []
description: "This series of Oracle tutorials will look at the use of sub-queries (non-correlated and correlated), views (join views, in-line views), joins (inner joins, outer joins, non-equi-joins and cross joins), and finally we'll look at the performance implications of various types of sql statements and how to ensure we don't inadvertently cause poor performance."
datePublished: '2016-04-28T12:18:43.707Z'
dateModified: '2016-04-28T12:18:33.629Z'
title: Advanced Oracle Tutorials - Go From Beginner To Expert With Real-World Examples
author: []
authors: []
publisher:
  name: null
  domain: null
  url: null
  favicon: null
starred: false
sourcePath: _posts/2016-04-28-advanced-oracle-tutorials-go-from-beginner-to-expert-with.md
published: true
url: advanced-oracle-tutorials-go-from-beginner-to-expert-with/index.html
_type: WebPage

---
# Advanced Oracle Tutorials - Go From Beginner To Expert With Real-World Examples

This series of Oracle tutorials will look at the use of sub-queries (non-correlated and correlated), views (join views, in-line views), joins (inner joins, outer joins, non-equi-joins and cross joins), and finally we'll look at the performance implications of various types of sql statements and how to ensure we don't inadvertently cause poor performance.

The first in our series of advanced Oracle tutorials focuses on the use of sub-queries in general and correlated sub-queries in particular.

## Sub Queries

Also known as nested queries, these are used to answer multi-part questions and are often interchangeable with a join. In fact, when executed, a SQL statement containing a sub-query may well be treated by Oracle exactly as if it were a join.

As an example let's assume we have in our Oracle database one table called

oracle\_tutorial

(which contains the names of all the tutorials we have and the authors id) and another table called

author

which links the author's names to his or her id.

These two tables would be defined as follows:

CREATE TABLE author

(author\_id NUMBER PRIMARY KEY

,author\_name VARCHAR2(30)

);

and

CREATE TABLE Oracle\_tutorial  
(tutorial\_id NUMBER PRIMARY KEY  
,tutorial\_name VARCHAR2(30)  
,author\_id NUMBER REFERENCES author(author\_id)  
);

Taking the trivial example of finding the titles of all the Oracle tutorials written by an author called Andy McKay, this could be expressed as either:

SELECT tutorial\_name FROM oracle\_tutorial WHERE author\_id =

(

SELECT author\_id FROM author 

WHERE author\_name = 'Andy McKay'

)

or

SELECT

tutorial\_

name

FROM oracle\_tutorial NATURAL JOIN author

WHERE author\_name = 'Andy McKay'

There would be little difference in terms of performance in this simple query, but for more complex queries there could well be performance implications so it is always worth trying a few variations and obtaining the execution plans for complex queries before deciding on any particular version.

## Oracle Tips & Tricks to   
SKYROCKET Your Career!

If you're not already a subscriber to Oracle Tips and Tricks, you're missing out on a myriad of tips and techniques to help you work better, faster and smarter. [Subscribe now to enhance your career.][0]

### Non Correlated Sub-Queries

The most common use of sub queries is in the WHERE clause of queries to define the limiting condition (i.e. what value(s) a column(s) must have to be of interest). This was shown in the above example. However, they can also be used in other parts of SQL statements, specifically:

* in the FROM clause of a SELECT statement instead of a table name (known as an in-line view);
* to provide the new values for the specified columns in an UPDATE statement.
* in INSERT, UPDATE and DELETE statements instead of a table name;
* in the WHERE, HAVING and START WITH clauses of SELECT, UPDATE and DELETE statements to define the limiting set of rows
* to define the set of rows to be included by a view or a snapshot in a CREATE VIEW or CREATE SNAPSHOT statement or the set of rows to be created in the target table of a CREATE TABLE AS or INSERT INTO statement;

The example shown earlier used a simple equality expression. In that case we were interested in only one row from the sub query. We can also use the sub query to provide a set of rows, though. For example, to find the names of all Oracle tutorials written by either Andy McKay or Nick Sale, the following SQL statement could be used:

SELECT

tutorial\_

name

FROM oracle\_tutorial WHERE author\_id IN

(

SELECT author\_id FROM author

WHERE author\_name IN ('Andy McKay','Nick Sale')

)

In fact, the original example could also return more than one row from the sub-query if there were two or more authors with the name Andy McKay in our set of Oracle tutorials. In that case, the first example would cause a run-time SQL error, though, because by using '=' we specified that the sub query should produce no more than one row (it is perfectly legitimate for a sub query to return no rows).

The question can also be reversed to ask for the names of all the Oracle tutorials that were NOT written by Andy McKay. To do this, the sense of the sub query just has to be reversed by prefixing it with 'NOT' or '!'.

SELECT

tutorial\_

name

FROM oracle\_tutorial WHERE author\_id

NOT IN

(

SELECT author\_id FROM author

WHERE author\_name = 'Andy McKay'

)

Or

SELECT

tutorial\_

name

FROM oracle\_tutorial WHERE author\_id

!=

(

SELECT author\_id FROM author

WHERE author\_name = 'Andy McKay'

)

sub-queries. This time we want to find the free cover limits of all ratings for all covers on all policies with an end date after 01-Jan-2009\. This could be written as follows:

SELECT free\_cover\_limit FROM rating

WHERE cover\_type IN

( SELECT cover\_type FROM cover\_type

WHERE policy\_no IN

( SELECT policy\_no FROM policy

WHERE end\_date \> '01-JAN-2009'))

Any of the other comparison operators instead of '=' or 'IN' such as '

The [next][1] in our series of Oracle tutorials will look at using sub-queries in the from clause and correlated sub-queries.  
Follow this link to learn about the various types of [SQL joins][2].

## Looking for instructor-led Oracle training?

[Learn Oracle ][3]with Smartsoft to advance your skills and sky rocket your career.

[Return][4] from advanced Oracle tutorials to asktheoracle.net home page

[][5][][5]

[0]: http://www.asktheoracle.net/oracle-tips-signup.html
[1]: http://www.asktheoracle.net/oracle-tutorials-advanced-2.html
[2]: http://www.asktheoracle.net/oracle-sql-joins.html
[3]: http://www.smart-soft.co.uk/oracle-and-unix-training.htm
[4]: http://www.asktheoracle.net/
[5]: http://www.asktheoracle.net/index.html