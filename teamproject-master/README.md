# GS1 Barcode Parser - by Group B

Contributors: Khaleb Groce, Aubrey Guidrey, Cade Carter, Bryson Leonard, David Pitts, and Andrew Brumbeloe 

This project is capable of parsing GS1 string barcodes.
These barcodes are found all over the world. GS1 is the standard set of barcodes that people use to help computers read and parse things.
To look at an exhaustice list of all items that can be parsed, please take a look at pages 135 through 139 of the Specification list below.

Here is a link to the codes that can be parsed from this program:   
[link to GS1 Specifications!](https://www.gs1.org/docs/barcodes/GS1_General_Specifications.pdf)

Each of the individual codes in this document have an object identifier that is at the front of every code that tells the program what the code contains and how to format it.

This application creates a master parsing object that recieves a string which contains a list of GS1 barcodes with the object identifier leading with relavant information following then may or not be separated by a "%" sign before the following code depending if the exact object has a known number of characters or numbers following the object identifier. 

The master parser object then determines the leading number of the object identifier and "passes off" the final parsing of invididual codes to classes that contain the information needed to determine the identifier type and how to format and display codes in the order they are given to the master parser. The classes are divided up into 8 different parsers that parse the codes that begin with the number in the name of the class. In other words, GS1_0X.java parses barcodes that have an identifier that begin with 0. GS1_3X.java parses codes that start with the number 3, and so on. 

-Example

0112345678901234 is a string that begins with 01 and then has 14 numeric characters afterward that contains information that is then parsed out and formatted by the following matching function.

GS1.java is an initial parser that searches for the leading number in the GS1 barcode and then hands off the rest of the code to the appropriate subclass.

super.matchers.put( "01", Pattern.compile("^01[0-9]{14}") ); // AI #01

This matcher searches for the 01 and then 14 numeric characters (as indicated by [0-9] which describes that it only accepts numbers and then {14} meaning exactly 14 total characters following the 01.

Common Errors-

If the number of characters following the object identifier is known or has an expected amount then a separator is not neccessary as the code will throw a "CODE INVALID" error if anything is missing or incorrectly formatted. If the number of characters following the identifier is not known, meaning it has a range of 5-30 characters, as an example, will be separated from the next code by a "%" or the program will throw a "CODE INVALID" error. If you recieve a code invalid error, then the string that is entered into the parser is either not formatted correctly or includes a code that is not described by the GS1 standard for barcodes. One of the most common ways this happens is caused by a missing % as the delimiter for a substring that can be a range of characters long and the parser is expecting that %.

