# RegEx (Regular Expression) Tutorial / breakdown 

This repo/gist will be discussing what a Regular Expression (RegEX for short) is and the process used to implement this function into your own application. 

## Summary

Briefly summarize the regex you will be describing and what you will explain. Include a code snippet of the regex. Replace this text with your summary.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

- - - -

### Anchors

Anchors are a different breed when it comes to the rest of the other regex symbols syntax. __*They do not match any character at all*__. Instead, they match a position before, after, or between characters. They can be used to “anchor” the regex match at a certain position.
  - For example, this is an email regex to verify a users email input ```/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/```. Now using a beginning ```^``` and ending ```$``` Anchor before the @ symbol would look like this ```/^([a-z0-9_\.-]+)$/```. 

Symbol  | Description
------------- | -------------
^  | The caret ^ matches the position before the first character in the string. Applying ^a to abc matches a. ^b does not match abc at all, because the b cannot be matched right after the start of the string, matched by ^.
$  | Similarly, $ matches right after the last character in the string. c$ matches c in abc, while a$ does not match at all.


- - - -
### Quantifiers

Example: if you are looking for matches for 4 digits, you can do ```/\d\d\d\d/```, or you can use quantifiers and do ```/\d{4}/```.

Symbol  | Description
------------- | -------------
{} | Quantifiers match a number of instances of a character, group, or character class in a string.
abc __{2,5}__ | matches a string that has __ab__ followed by 2 up to 5 __c__

```
let str = 'ECMAScript 2020';
let re = /\d{4}/;

let result = str.match(re);

console.log(result);
```

Output will be ```2020```

- - - -
### OR Operator

OR operator uses ```|``` or ```[]``` to match either or of a character. For example, ```a(b|c)``` matches a string that has a followed by ```b``` or ```c``` __(and captures b or c)__. 

a[bc] same as previous, but without capturing b or c

Symbol  | description
------------- | -------------
[ ]  | Character classes matches any single character in a range or set enclosed in square  brackets. For example, [aeiou] matches any vowel. You can also use a shorthand notation for a range of characters. For example, [0-9] matches any decimal digit. If the sequence is preceded by a carat:    ^   it matches any single character NOT from the range or set. For example, [^a-z] matches any character that is not a letter in the alphabet.

- - - -
### Character Classes

Character classes have a ```/``` in the front of a letter, and depending on the letter, will dictate what you will try to match. 

Symbol  | Description
------------- | -------------
\d  | matches a single digit characters.
\w  | matches any word character. (selects every word, NOT spaces(or whitespace as it is sometimes referred too as) or digits or special characters(!@#$%^&*-+))
\s  | matches any spaces between characters.
```\.```  | matches all and any characters. 

- - - -
### Flags

A flag changes the default searching behavior of a regular expression. It makes a regex search in a different way. With the ```i``` flag set, lowercase/uppercase characters match in the string.

Symbol  | Description
------------- | -------------
i  | __Ignore Casing__ is a Boolean and initially is set to true. If the ```i``` flag is used, then it becomes false. The ```i``` flag indicates that case should be ignored while attempting a match in a string. 
g  | __Global Search__ serves to make an expression look for all its matches, rather than stopping at the first one. By default, when a regex engine finds the first match for a given pattern in a given test string, it terminates right at that point without looking any further. 
s  | __Dot all__ (the wildcard) matches all possible characters. By default, the dot character in a regular expression matches everything, but newline characters. To get it to match newline characters as well, we are given the s flag. the 's' is an abbreviation for __*single-line mode*__. 
m  | Content Cell
y  | Content Cell
u  | Content Cell

- An example for __Ignore Casing__ would be: 
```
var str = "Hello world! This 'Hello World' convention is quite common in introducing programming languages."; 
var regex = /hello/i; 
var newStr = str.replace(regex, '(Hello)');
```
Output would be: "world! This 'World' convention is quite common in introducing programming languages."

- An example for __Global Search__ would be:
```
var str = "50 is the half of 50 x 2 that is 80.";
var newStr = str.replace(/50/g, "40");
console.log(newStr);
```
Output would be: "40 is the half of 40 x 2 that is 80."


- An example for __Dot all__ would be:
```
The first expression /.+/g without the s flag will match every single line in str. The __bolded__ portions shown below represent the matches:

"__Content flows__\n __downward and__ \n __downward__"

The second expression /.+/gs with the s flag will make . match every character including \n, which means that the expression will match the whole string str, as shown below:

"Content flows\ndownward and\ndownward"
```

Output would be:


- An example for __Ignore Casing__ would be:
```

```

Output would be:


- An example for __Ignore Casing__ would be:
```

```

Output would be:


- An example for __Ignore Casing__ would be:
```

```

Output would be:


- - - -
### Grouping and Capturing

Symbol  | Description
------------- | -------------
Content Cell  | Content Cell

- - - -
### Bracket Expressions

Symbol  | Description
------------- | -------------
Content Cell  | Content Cell

- - - -
### Greedy and Lazy Match

Symbol  | Description
------------- | -------------
Content Cell  | Content Cell

- - - -
### Boundaries

Symbol  | Description
------------- | -------------
Content Cell  | Content Cell

- - - -
### Back-references

Symbol  | Description
------------- | -------------
Content Cell  | Content Cell

- - - -
### Look-ahead and Look-behind

Symbol  | Description
------------- | -------------
Content Cell  | Content Cell

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
