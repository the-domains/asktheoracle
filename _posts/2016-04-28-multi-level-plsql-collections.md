---
inFeed: true
hasPage: true
inNav: false
inLanguage: null
keywords: []
description: "PL/SQL collections are very useful for modeling more complex or sophisticated data types such as the array, table or set types that exist in other languages. We've seen in previous tutorials that Oracle has 3 types of collections in PL/SQL"
datePublished: '2016-04-28T10:18:10.812Z'
dateModified: '2016-04-28T10:18:10.106Z'
title: Multi Level PL/SQL Collections
authors: []
publisher:
  name: null
  domain: null
  url: null
  favicon: null
author: []
starred: false
sourcePath: _posts/2016-04-28-multi-level-plsql-collections.md
published: true
url: multi-level-plsql-collections/index.html
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

* [nested tables of associative arrays][0] and [vice versa][1]
* nested tables of varrays and [vice versa][2]

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

It is worth pointing out that we could achieve more or less the same effect just by having an associative array of varchar2 indexed by varchar2, however each element of the array would have to be a concatenation of the relevant tutorial's topics - as per the following example.

DECLARE

TYPE tutorial\_tab IS TABLE OF VARCHAR2(200)

INDEX BY VARCHAR2(200); 

tutorials tutorial\_tab; -- single dimension plsql collection 

BEGIN

tutorials('Multi Dimensional PL/SQL Collection') :=

'PLSQL Nested Tables PL/SQL Associative Arrays');

tutorials('PL/SQL Loops') :=

'PLSQL Cursor For Loops PL/SQL While Loops Infinite Loops');

/\* let's see what we've got \*/

DBMS\_OUTPUT.PUT\_LINE(

'Multi Dimensional PL/SQL Collection topics: '|| tutorials('Multi Dimensional PL/SQL Collection'));

DBMS\_OUTPUT.PUT\_LINE(

'Topics covered by PL/SQL Loops tutorial: '||

tutorials('PL/SQL Loops'));

END;

/

The output should be as follows:

Multi Dimensional PL/SQL Collection topics: PLSQL Nested Tables PL/SQL Associative Arrays

Topics covered by PL/SQL Loops tutorial: PLSQL Cursor For Loops PL/SQL While Loops Infinite Loops

## 2 Dimensional PL/SQL Collection - Nested Table of Associative Array 

In this example our first level is an associative array to hold the topics associated with each tutorial and the next level holds the version numbers of the tutorials. This means each element of the nested table (the top level) holds the tutorial names and the topics of each tutorial.

DECLARE

TYPE tutorial IS TABLE OF VARCHAR2(2000) 

INDEX BY VARCHAR2(200); 

tutorials tutorial\_tab; -- single dimension plsql collection 

TYPE tutorial\_version\_tab IS TABLE OF tutorial\_tab; 

tutorial\_versions tutorial\_version\_tab;

-- multi dimensional plsql collection 

BEGIN

/\* create collection of topics for first tutorial \*/

tutorials('PLSQL Collections') :=

'PL/SQL Nested Tables, PL/SQL Associative Arrays');

/\* create collection of topics for second tutorial \*/

tutorials('PL/SQL Loops') :=

'PLSQL Cursor For Loops, PL/SQL While Loops, Infinite Loops');

tutorial\_versions := tutorial\_version\_tab(tutorials);

/\* need to use the constructor as 

tutorial\_versions is a nested table.

This populates tutorial\_versions(1) \*/

/\* we can now re-use tutorials for the 2nd version \*/

tutorials('PLSQL Collections') := 'PLSQL Nested Tables';

tutorials('PL/SQL Loops' ) := 'PLSQL Cursor For Loops';

tutorial\_version.EXTEND; -- now has 2 cells

tutorial\_version(2) := tutorials;

-- assign whole collection (tutorials) to cell 2

/\* now let's see what we've got \*/

DBMS\_OUTPUT.PUT\_LINE('Previous topics in PL/SQL Loops: '||

tutorial\_versions(2)('PL/SQL Loops');

DBMS\_OUTPUT.PUT\_LINE(

'Latest version of PL/SQL Loops tutorial: '||

tutorial\_versions(1)('PL/SQL Loops');

DBMS\_OUTPUT.PUT\_LINE(

'Previous topics in PLSQL Collections: '||

tutorial\_versions(2)('PL/SQL Collection');

DBMS\_OUTPUT.PUT\_LINE(

'Latest version of PLSQL Collections tutorial: '||

tutorial\_versions(1)('PL/SQL Collection');

END;

/

Output:

Previous topics in PL/SQL Loops: PLSQL Cursor For Loops

Latest version of PL/SQL Loops tutorial: PLSQL Cursor For Loops, PLSQL While Loops, Infinite Loops

Previous topics in PL/SQL Collections: PLSQL Nested Tables

Latest version of PL/SQL Collections tutorial:PLSQL Nested Tables, Associative Arrays

**Oracle Tips & Tricks to SKYROCKET Your Career!**

If you're not already a subscriber you're missing out on a myriad of tips and techniques to help you become a better, faster, smarter developer.[Subscribe now][4]and ignite your career.

## 3 Dimensional PL/SQL Collection of an Associative Array of Nested Tables of Varrays

This example demonstrates that we can have three levels in our collection. This time let's assume we want to store information about the topics of Oracle and PL/SQL training courses. Each course has one or more sessions and each session has one or more topics.

To achieve this we'll make the first layer a nested table to contain the courses, the next level is a varray (each course can have up to 30 sessions) and the top level is an associative array so that we can store the names of the training courses. 

DECLARE

TYPE topic\_ty IS TABLE OF VARCHAR2(200);

TYPE session\_ty IS VARRAY(30) OF topic\_ty;

TYPE course\_tab IS TABLE OF session\_ty INDEX BY VARCHAR2(80);

training\_course course\_tab; -- a plsql collection variable

BEGIN

training\_course('Oracle') := 

session\_ty

(

/\*session(1) \*/

topic\_ty( 

'Relational database concepts' -- topic \# 1

,'Database administration tasks' -- topic \# 2

,'DBA responsibilities' -- topic \# 3 )

,topic\_ty(

/\*session(2) \*/

'Oracle architecture'

,'Oracle instance'

,'memory structures'

,'background processes'

,'server and client processes' ,'Oracle database'

)

,topic\_ty(

/\* session(3) \*/

'installation prerequisites'

,'system requirements'

,'optimal flexible architecture'

,'database authentication methods'

,'Oracle environment variables'

,'installation using the Oracle Universal Installer'

,'using database configuration assistant'

,'using database upgrade assistant'

)

,topic\_ty(

/\* session(4) \*/

'administration tools'

,'database management with SQL\*Plus'

,'using Enterprise Manager'

)

);

training\_course('PL/SQL'):= 

session\_ty(

topic\_ty(

'basic elements of PL/SQL'

,'variables and constants'

,'PLSQL data types'

)

);

/\* now collection has been initialised

we can access a specific element \*/

training\_course('Oracle')(4) := 

topic\_ty('overview of network configuration'

,'listener configuration and management'

,'Oracle net naming methods'

,'starting/stopping the listener'

,'using TNSPING to test Oracle net connectivity'

); -- overwrite whole collection (session 5)

DBMS\_OUTPUT.PUT\_LINE(

'2nd topic of 3rd session of Oracle course= '||

training\_course('Oracle')(3)(2));

END;

/

Output:

2nd topic of 3rd session of Oracle course = system requirements

If you attempt to read from or write to an un-initialized nested table or varray Oracle raises an exception so in the above example we have to initialize the underlying elements of the varray and the nested table before we can access a particular cell in the (top level) associative array.

When we're constructing the collection we have to nest the constructors - each session consists of a set of topics, so each new set of topics is therefore a new session.

We could go on to add a fourth dimension by splitting training courses into one or more days of one more sessions of one or more topics - but that starts to get very complicated so we'll leave that as an exercise for you!

## 3 Dimensional PL/SQL Collection of an Associative Array of Associative Arrays of Nested Tables

In this final example, let's change the previous example so that we can have a name rather than a number for each session of each course.

DECLARE

TYPE topic\_ty IS TABLE OF VARCHAR2(200);

TYPE session\_ty IS TABLE OF topic\_ty INDEX BY VARCHAR2(80);

TYPE course\_tab IS TABLE OF session\_ty

INDEX BY VARCHAR2(80);

training\_course course\_tab; -- a pl/sql collection variable

BEGIN

training\_course('Oracle')('Introduction to Oracle 10g') := 

topic\_ty( 

/\*session(1) \*/

'Relational database concepts' -- topic \# 1

,'Database administration tasks' -- topic \# 2

,'DBA responsibilities' -- topic \# 3

);

training\_course('Oracle')('Oracle 10g architecture') := 

topic\_ty( 

/\*session(2) \*/

'Oracle architecture'

,'Oracle instance'

,'memory structures'

,'background processes'

,'server and client processes' ,'Oracle database'

);

training\_course('Oracle')('installation/configuration') := 

topic\_ty( 

/\* session(3) \*/

'Oracle installation prerequisites'

,'system requirements'

,'optimal flexible architecture'

,'database authentication methods'

,'Oracle environment variables'

,'installation using the Oracle Universal Installer'

,'using database configuration assistant'

,'using database upgrade assistant'

);

training\_course('Oracle')('database administration') := 

topic\_ty( 

/\* session(4) \*/

'administration tools'

,'database management with SQL\*Plus'

,'using Enterprise Manager'

);

training\_course('PL/SQL')('Session 1') := 

topic\_ty( 

'basic elements of PL/SQL'

,'variables and constants'

,'PLSQL data types'

);

DBMS\_OUTPUT.PUT\_LINE(

'1st topic of 3rd session of Oracle course= '||

training\_course('Oracle')('installation/configuration')

(1));

END;

/

1st topic of 3rd session of Oracle course=Oracle installation prerequisites

Notice this time that we have to populate each cell of the top level associative array separately (in a new statement) which can make the PL/SQL code a little more unwieldy but it does make it clearer.

[Back to nested tables][5][On to PL/SQL Collections of Records][6]

[**Learn PL/SQL**][7]**from the experts and boost your career with**[**instructor-led or on-demand Oracle PL/SQL training**][7]

[0]: http://www.asktheoracle.net/multi-level-plsql-collections.html#Nested_Table_of_Associative_Array_
[1]: http://www.asktheoracle.net/multi-level-plsql-collections.html#PLSQL_Collections_of_Associative_Array
[2]: http://www.asktheoracle.net/multi-level-plsql-collections.html#PLSQL_Collections_of_Associative_Array_
[3]: http://www.asktheoracle.net/multi-level-plsql-collections.html#Associative_Array_of_Associative_Array
[4]: http://www.asktheoracle.net/oracle-tips-signup.html
[5]: http://www.asktheoracle.net/plsql-collections-part-3.html
[6]: http://www.asktheoracle.net/plsql-collections-of-records.html
[7]: http://www.asktheoracle.net/oracle-training.html