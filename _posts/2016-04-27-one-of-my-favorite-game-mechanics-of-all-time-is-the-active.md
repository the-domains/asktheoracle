---
inFeed: true
hasPage: true
inNav: false
inLanguage: null
keywords: []
description: "PL/SQL collections are very useful for modeling more complex or sophisticated data types such as the array, table or set types that exist in other languages. We've seen in previous tutorials that Oracle has 3 types of collections in PL/SQL"
datePublished: '2016-04-28T10:10:53.021Z'
dateModified: '2016-04-28T09:45:43.059Z'
title: 'Multi Level PL/SQL Collections '
author:
  - name: ''
    url: ''
sourcePath: _posts/2016-04-27-one-of-my-favorite-game-mechanics-of-all-time-is-the-active.md
published: true
authors: []
publisher:
  name: null
  domain: null
  url: null
  favicon: null
starred: false
url: one-of-my-favorite-game-mechanics-of-all-time-is-the-active/index.html
_type: Article

---
# Multi Level PL/SQL Collections 

PL/SQL collections are very useful for modeling more complex or sophisticated data types such as the array, table or set types that exist in other languages. We've seen in previous tutorials that Oracle has 3 types of collections in PL/SQL

1. associative arrays (also known as index-by tables)
2. VARRAYs (varying size arrays)
3. nested tables

However these types are only single dimensional. 

What do we if we need multi dimensional pl/sql collections?

Simple, we just create collections of collections and they don't need to be of the same type, so we can have:-

* [nested tables of associative arrays][0]and[vice versa][1]
* nested tables of varrays and[vice versa][2]

* varrays of associative arrays and vice versa
* varrays of varrays
* [associative arrays of associative arrays][3]
* nested tables of nested tables

We are not limited to two levels (dimensions) either, we can create as many levels as we like (subject to memory constraints) however the more levels we add the more complex the code becomes.

Let's have a look at a few examples. 

## 2 Dimensional PL/SQL Collection of an Associative Array of Nested Tables

Let's suppose we have a number of Oracle and PL/SQL tutorials and we wish to keep track of the topics covered in the tutorials.

Our first level, therefore, would be a nested table of type varchar2 to hold the topics for each tutorial. The next level would hold the names of the tutorials.

Therefore the code might look something like the following.

DECLARE

TYPE topic\_tab IS TABLE OF VARCHAR2(20); -- first level 

TYPE tutorial\_tab IS 

TABLE OF topic\_tab INDEX BY VARCHAR2(20); 

tutorials tutorial\_tab; 

-- multi dimensional plsql collection 

BEGIN

tutorials('PL/SQL Collection') :=

topic\_tab('PLSQL Nested Tables'

,'PL/SQL Associative Arrays'

);

/\* need to use the constructor as 

1st level is a nested table \*/

tutorials('PL/SQL Loops') :=

topic\_tab('PLSQL Cursor For Loops'

,'PL/SQL While Loops'

,'Infinite Loops'

);

/\* let's see what we've got \*/

DBMS\_OUTPUT.PUT\_LINE(

'Multi Dimensional PL/SQL Collection topics: ');

DBMS\_OUTPUT.PUT\_LINE(

tutorials('Multi Dimensional PL/SQL Collection')(1)||', '||

tutorials('Multi Dimensional PL/SQL Collection')(2)); 

DBMS\_OUTPUT.PUT\_LINE(

'Topics covered by PL/SQL Loops tutorial: '||

tutorials('PL/SQL Loops')(1)||', '||

tutorials('PL/SQL Loops')(2)||', '||

tutorials('PL/SQL Loops')(3)); 

END;

/

The Output for this should be:

Multi Dimensional PL/SQL Collection topics:

PLSQL Nested Tables, PL/SQL Associative Arrays

Topics covered by PL/SQL Loops tutorial: PLSQL Cursor For Loops, PL/SQL While Loops, Infinite Loops

[0]: http://www.asktheoracle.net/multi-level-plsql-collections.html#Nested_Table_of_Associative_Array_
[1]: http://www.asktheoracle.net/multi-level-plsql-collections.html#PLSQL_Collections_of_Associative_Array
[2]: http://www.asktheoracle.net/multi-level-plsql-collections.html#PLSQL_Collections_of_Associative_Array_
[3]: http://www.asktheoracle.net/multi-level-plsql-collections.html#Associative_Array_of_Associative_Array