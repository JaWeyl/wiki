[Source](https://www.youtube.com/watch?v=sa-TUpSx1JA&t=1385s)
# Regular Expressions
Learn how to match patterns of text.

## MetaCharacters
Are characters that need to be *escaped* since those are special characters in regular expressions.
```
.[{()\^$|?*+
```
Now to search for them explicitly we have to escape them
by putting ```\``` in front of them
```
\.
```
searches only for the literal ```.``` search

## Groups
Groups can be used to search for several different pattern.

# Examples
- Phone numbers
  ```
  321-555-4321
  123.555.1234
  123*555*1234
  700.555.1234
  900.555.1234
  800.555.1234
  900.555.1234
  
  ```
  ```
  \d{3}[-.]\d{3}[-.]\d{3,4}
  [7-9]0{2}[-.]\d{3}[-.]\d{3,4}
  ```
- Names
  ```
  Mr. Schafer
  Mr Smith
  Ms Davis
  Mrs. Robinson
  Mr. T
  ```
  ```
  M(r|s|rs)?\.?\s\w*
  M[r|s|rs]?\.?\s\w*
  ```
- Emails
  ```
  CoreyMSchafer@gmail.com
  corey.schafer@university.edu
  corey-321-schafer@my-work.net
  ```

  ```
  [a-zA-Z0-9.-]+@[a-z-]+\.(com|edu|net)
  ```
- URLs
  ```
  https://www.google.com
  http://coreyms.com
  https://youtube.com
  https://www.nasa.gov 
  ``` 
  ```
  https?://(www\.)?\w+\.\w+
  https?://(www\.)?(\w+)(\.\w+)
  ```


# Snipptes
```
.       - Any Character Except New Line
\d      - Digit (0-9)
\D      - Not a Digit (0-9)
\w      - Word Character (a-z, A-Z, 0-9, _)
\W      - Not a Word Character, e.g., meta characters
\s      - Whitespace (space, tab, newline)
\S      - Not Whitespace (space, tab, newline)

\b      - Word Boundary
\B      - Not a Word Boundary
^       - Beginning of a String/Line
$       - End of a String/Line

[]      - Matches Characters in brackets (Character Set)
          to define a range use [1-9], [a-z],[A-Z] 
[^ ]    - Matches Characters NOT in brackets
|       - Either Or
( )     - Group

Quantifiers:
*       - 0 or More
+       - 1 or More
?       - 0 or One
{3}     - Exact Number
{3,4}   - Range of Numbers (Minimum, Maximum)
```
First define the search pattern and afterwards the *quantifier*, e.g.:
```
[0-9]?
```