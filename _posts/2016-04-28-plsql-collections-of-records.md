---
inFeed: true
hasPage: true
inNav: true
inLanguage: null
keywords: []
description: ''
datePublished: '2016-04-28T16:37:05.970Z'
dateModified: '2016-04-28T16:36:14.832Z'
title: 'PL/SQL Collections of Records '
author: []
authors: []
publisher:
  name: null
  domain: null
  url: null
  favicon: null
starred: false
sourcePath: _posts/2016-04-28-plsql-collections-of-records.md
published: true
url: plsql-collections-of-records/index.html
_type: Article

---
# PL/SQL Collections of Records 

PL/SQL collections can be very useful for modeling more complex or sophisticated data types such as the array, table or set types that exist in other languages and Oracle PL/SQL provides us with 3 types of collections:

1. [associative arrays][0](also known as index-by tables)
2. [VARRAYs][1](varying size arrays)
3. [nested tables][2]

We can also have [m][3][ulti dimensional pl/sql collections][3]. But what do we if we need collections of complex data types rather than the simple data types of varchar2, char, or number?

Fortunately, PL/SQL allows us to define our own complex data types by using the record structure and to create collections of records, enabling us to build very sophisticated data structures as we'll see shortly.

Let's start with a straightforward example of creating and using a PL/SQL record and a collection of records.

## Example 1: Defining and Using a PL/SQL record structure

DECLARE

TYPE book\_typ IS RECORD

(

isbn         VARCHAR2(20)  

,title        VARCHAR2(2000)

,author       VARCHAR2(2000)

,publisher    VARCHAR2(120) 

,published\_on DATE

);

TYPE books\_tab IS TABLE OF book\_typ; -- nested table

books    books\_tab;

a\_book   book\_typ;

BEGIN

a\_book.title        :=

'Oracle Database 10g Performance Tuning Tips and Techniques';

a\_book.author       := 'Richard Niemiec';

a\_book.publisher    := 'McGraw-Hill Osborne Media';

a\_book.isbn         := '978-0072263053';

a\_book.published\_on :=

to\_date('30 July 2007','dd mon yyyy');

books                 := books\_tab(a\_book);

END;

In this example we define our data types first (as always). In this case our type

books\_tab

has multiple components so we first need declare a record structure (

book\_typ

) to hold them. We can now use this record type in our declarations for our pl/sql collections. In this case the collection type (

books\_tab

) is a nested table type of the just defined record type. This enables us to have multiple records which, as we'll see shortly, allows us to read pl/sql collections from and write them to our Oracle database in one operation.

Having defined our types we need to declare variables of those types to be able to use them. We define one variable

books

which is a pl/sql collection and another variable

a\_book

which is able to hold one instance of the record type

book\_typ

declared earlier.

Accessing the components in the p/lsql record is straight forward as each component has a name so it's just the variable name followed by the component name.

For example, the author field is accessed by the following statement:

a\_

book.author := 'Richard Niemiec';

Having populated our record we can then use this to initialise our nested table collection as each cell in the collection has the same structure as the record variable. To instantiate nested table type Oracle pl/sql collections we have to use the constructor routine which is the type name (see the tutorial on [nested tables][2] for more details). In this example we populate it with just 1 element (record). To add more we would use the extend method and then populate the new elements in a similar manner.

## Oracle Tips & Tricks to SKYROCKET Your Career!

If you're not already a subscriber you're missing out on a myriad of tips and techniques to help you become a better, faster, smarter developer.

[Subscribe now][4]

and ignite your career.

## Example 2: Defining and Using a PL/SQL record structure in a multi-dimensional collection

DECLARE

TYPE author\_typ IS TABLE OF VARCHAR2(120);

TYPE book\_rec IS RECORD

(

isbn         VARCHAR2(20)

,title        VARCHAR2(2000)

,author       author\_typ

,publisher    VARCHAR2(120)

,published\_on DATE

);

TYPE book\_tab IS TABLE OF book\_rec;

TYPE book\_set\_typ IS TABLE OF book\_tab INDEX BY VARCHAR2(200);

book     book\_rec;

book\_set book\_set\_typ; --plsql multi-level collection variable

BEGIN

book.title        :=

'OCA: Oracle Database 11g Certfied Associate Study Guide';

book.author       :=

author\_typ('Biju Thomas'

,'Robert G. Freeman'

,'Charles A. Pack'

,'Doug Sturns'

);

book.publisher    := 'Sybex';

book.isbn         := '978-0470395141';

book.published\_on := TO\_DATE('13 April 2009','dd mon yyyy');

book\_set('OCP Oracle 11g Certifcation Kit') :=

book\_tab(book,book);

-- intialise 1st book\_set with 2 books (the same)

book\_set('OCP Oracle 11g Certifcation Kit')(2).title :=

'OCP: Oracle 11g Certfied Professional Study Guide';

-- correct title of 2nd book in the set

book\_set('OCP 10g Certifcation Kit') := book\_tab(book,book);

-- intialise 2nd book\_set with 2 books (the same)

book\_set('OCP 10g Certifcation Kit')(2).author(1) :=

'Tim Buterbaugh';

book\_set('OCP 10g Certifcation Kit')(1).author :=

author\_typ('Tim Buterbaugh'

,'Chip Dawes'

,'Bob Bryla'

,'Doug Stuns'); 

book\_set('OCP 10g Certifcation Kit')(2).title :=

'OCP: Oracle 10g Certfied Professional Study Guide';

-- change title of 2nd book in the set

END;

As in the previous example, our base data type has multiple components so we need to declare a record structure (

book\_rec

) to hold them. However, this time each book can have multiple authors by vrtue of having defined the author field as a nested table collection (

author\_type

). We could also have used a VARRAY collection if we wished to limit the maximum number of authors a book can have.

The next declaration (

books\_tab

) is another example of nested table Oracle pl/sql collections. In this case it is a nested table type collection of the just defined record type (

book\_rec

). This enables us to store details of multiple books. However in this example we take it a step further by declaring an associative array type collection which enables to store sets (collections) of books.

With the types (data structures) defined we can declare variables of those types so that we can use them. We define one variable book which holds one instance of the record type (

book\_rec

) we declared earlier and the variable

book\_set

to hold the details of our sets (collections) of books

The next step is to populate the fields (attributes) of the book (the PL/SQL record) and then use this to initialise our collection. The following statement

book\_set('OCP Oracle 11g Certifcation Kit') :=

book\_tab(book,book);

creates one element in our top level associative array and creates and initialises two elements in the nested table pl/sql collection. This has the effect of creating one set of two books, although both books are initially the same. Next we change the title of the second book in our first set with this statement

book\_set('OCP

Oracle

11g Certifcation Kit')(2).title :=

'OCP: Oracle 11g Certfied Professional Study Guide';

-- correct title of 2nd book in the set

Next, we create a second set of books (again initially both books have all the same details) and change the name of the 1st author of the 2nd book with this statement:

book\_set('OCP 10g Certifcation Kit')(2).author(1) :=

'Tim Buterbaugh';

Note that all the other author names remain unchanged.

The next statement uses the nested table constructor to re-initialise the (set of) authors' names of the first book in the second set.

book\_set('OCP 10g Certifcation Kit')(1).author :=

author\_typ('Tim Buterbaugh'

,'Chip Dawes'

,'Bob Bryla'

,'Doug Stuns'); 

Finally we change the title of the second book in the second set of books.

book\_set('OCP 10g Certifcation Kit')(2).title :=

'OCP: Oracle 10g Certfied Professional Study Guide';

## Example 3: Reading/Writing PL/SQL collections From/To Oracle

In this example we define a record type the components of which are anchored to the definitions of columns in the database by use of %TYPE, plus a collection of records defined impilicitly and anchored to the definition of the employees table in our Oracle database by use of %ROWTYPE.

DECLARE

TYPE dept\_rec IS RECORD

(

dept\_id   departments.department\_id%TYPE

,dept\_name departments.department\_name%TYPE

); -- anchor definitions to reduce maintenance

TYPE numtab IS TABLE OF employees%ROWTYPE;

-- each element is same type as row in employees table

dept dept\_rec; -- single record variable

emps numtab; -- nested table pl/sql collection

BEGIN

/\* retrieve name and id of just 1 department \*/

SELECT department\_id,department\_name

INTO dept.dept\_id, dept.dept\_name

FROM departments WHERE ROWNUM < 2;         

/\*

use of bulk collect and forall with collections can

significately improve performance of Oracle pl/sql code

\*/

SELECT \* BULK COLLECT INTO emps FROM employees; 

-- retrieve all employee details from Oracle in one hit

FOR i IN emps.FIRST .. emps.LAST LOOP

dbms\_output.put\_line(

'emps('||i||').employee\_id = '||emps(i).employee\_id

);

END LOOP;     

FORALL J IN emps.FIRST .. emps.LAST

INSERT INTO emp2 values emps(j);

-- insert all employee details into

-- database table emp2 in one hit

END;

The variable

dept

(which is a record type) is populated by reading columns of one row of the departments table and assigning them to the components of the record.

For PL/SQL collections, Oracle provides the

bulk collect

option to populate the collection using just one statement, however we can still access individual elements of our collection using the index. Writing the collection to the database can be done either one element at a time (using a loop) or all in one go by use of the

FORALL

statment.

[Back to multi-dimensional pl/sql collections][3]

On to

[use of explicit cursors][5]

Looking for Oracle PL/SQL training courses?

[Learn PL/SQL][6]

from the experts and sky-rocket your career with top quality

[Oracle PL/SQL training][6]

.

[Return to PL/SQL overview][7]  
[Return to home page][8]

[0]: http://www.asktheoracle.net/plsql-collections-associative-arrays.html
[1]: http://www.asktheoracle.net/plsql-collections-part-2.html
[2]: http://www.asktheoracle.net/plsql-collections-part-3.html
[3]: http://www.asktheoracle.net/multi-level-plsql-collections.html
[4]: http://www.asktheoracle.net/oracle-tips-signup.html
[5]: http://www.asktheoracle.net/plsql-tutorial-using-cursors.html
[6]: http://www.asktheoracle.net/oracle-training.html
[7]: http://www.asktheoracle.net/plsql-tutorial.html
[8]: http://www.asktheoracle.net/index.html