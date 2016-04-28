---
inFeed: true
hasPage: true
inNav: true
inLanguage: null
keywords: []
description: This is the first PL/SQL tutorial in the series and provides an overview of the language and its capabilities as well as links to enable you to explore further.
datePublished: '2016-04-28T11:15:00.185Z'
dateModified: '2016-04-28T11:14:42.825Z'
title: What is PL/SQL?
author: []
authors: []
publisher:
  name: null
  domain: null
  url: null
  favicon: null
starred: false
sourcePath: _posts/2016-04-28-what-is-plsql.md
published: true
url: what-is-plsql/index.html
_type: Article

---
![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/e463920b-d332-4062-b842-4f10a45670b7.jpg)

# Oracle PL/SQLTutorial -A Whistle Stop Tour

This is the first PL/SQL tutorial in the series and provides an overview of the language and its capabilities as well as links to enable you to explore further.

In this tutorial we'll answer the following questions:

* what is PL/SQL? 
* What can it do?

## What is PL/SQL?

Learn the fundamentals of PL/SQL in our short video which shows you how to write a program to display "Hello World" in about 30 seconds!

https://www.youtube.com/watch?feature=player\_embedded&v=iY-X5O1ellQ

PL/SQL is Oracle's proprietary,

block-structured, strongly-typed, procedural programming language for manipulating data and interacting with the database.

The procedural part is important - the language provides you with all the things that SQL lacks like user-defined functions, loops, control statements (though SQL does provide some control in the form of the CASE clause, and the DECODE and NVL functions.). In fact the name stands for "Procedural Language extensions to the Structured Query Language".

Overall PL/SQL is a high-level language very similar to Pascal and ADA (from which it is derived). As Pascal was designed as a teaching language, this makes it easy to learn and to use and it promotes good programming practice. Although it is still possible to write bad code you just have to try that bit harder to do so!

# Oracle Tips & Tricks to SKYROCKET Your Career!

# If you're not already a subscriber to our newsletteryou're missing out on myriad of tips and techniques to help you become a better, faster, smarter developer. [Subscribe now][0] and ignite your career

PL/SQL has been described as the poor man's object-oriented language, but that was harsh even before the specific object-oriented features were added in Oracle8\. It is a very powerful and flexible language which, whilst not strictly object-oriented like Java, still has some o-o features, such as encapsulation, data hiding, inheritance, object types etc.

However, not all object-oriented features are available in all versions of PL/SQL The higher the version you're using, the more o-o features are available. Coverage of the object-oriented features has been deferred to a separate tutorial.

## What can you do with PL/SQL?

What can you do with it? The answer is plenty.

As hinted at earlier, you can define your own functions which can be embedded in SQL statements in the same way as the built-in functions.

You can also use it to write complete programs to implement business logic, furthermore you can store these programs in the database itself (and take advantage of the extra power of the server) or in Oracle Forms and Reports.

Stored procedures can be invoked from SQL, or other languages such as Java, C, FORTRAN or Visual Basic (these topics are outside the scope of this PL/SQL tutorial).

In short there is little that you can't do - as long as you don't need fancy i/o or file handling features. The only language element for displaying information directly to the end-user is the DBMS\_OUTPUT package, whilst the (limited) file handling capabilities are provided by the UTL\_FILE package. 

That was just a brief overview of the language - this PL/SQL tutorial continues with 

* [language elements][1]
* [PL/SQL tutorial part 2 - why and when should you use PL/SQL?][1]
* [examples of using Loops][2]
* [functions][3]
* [procedures][4]
* [integration with the Oracle database][5]
* [PL/SQL collections part 1 - associative arrays][6]
* [collections part 2 - varrays][7]
* [collections part 3 - nested tables][8]
* [multi level collections][9]
* [collections of records][10]
* [examples of using implicit cursors][11]
* [using explicit cursors][12]
* [PL/SQL tuning and optimisation][13]
* [What are the 7 worst coding crimes you can commit?][14]
* [What are the biggest myths about PL/SQL performance?][15]
* [What are the best practices?][16]

[0]: http://www.asktheoracle.net/oracle-tips-signup.html
[1]: http://www.asktheoracle.net/plsql-tutorial-part1.html
[2]: http://www.asktheoracle.net/oracle-plsql-tutorial-loops.html
[3]: http://www.asktheoracle.net/plsql-function.html
[4]: http://www.asktheoracle.net/plsql-procedure.html
[5]: http://www.asktheoracle.net/plsql-tutorial-part2.html
[6]: http://www.asktheoracle.net/plsql-collections-associative-arrays.html
[7]: http://www.asktheoracle.net/plsql-collections-part-2.html
[8]: http://www.asktheoracle.net/plsql-collections-part-3.html
[9]: http://www.asktheoracle.net/plsql-tutorial.html#content_3625679
[10]: http://www.asktheoracle.net/plsql-collections-of-records.html
[11]: http://www.asktheoracle.net/plsql-tutorial-using-cursors.html
[12]: http://www.asktheoracle.net/plsql-tutorial-using-explicit-cursors.html
[13]: http://www.asktheoracle.net/oracle-plsql-performance-tuning.html
[14]: http://www.asktheoracle.net/plsql-tutorial-7-crimes.html
[15]: http://www.asktheoracle.net/plsql-myths.html
[16]: http://www.asktheoracle.net/plsql-best-practice.html