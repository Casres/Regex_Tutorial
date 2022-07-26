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
s  | __Dot all__ (***the wildcard***) matches all possible characters. By default, the dot character in a regular expression matches everything, but newline characters. To get it to match newline characters as well, we are given the s flag. the 's' is an abbreviation for __*single-line mode*__. 
m  | __multiline mode__ serves to make the boundary tokens (```^``` and ```$```) match the beginning and end of each line. By default, the (```^``` and ```$```) characters, in an expression, match the beginning and ending boundaries of a given test string that the expression is on. But with the ```m``` flag in place, __they__ instead __do this for every line in the string__. A more controlled flag from ```s```.
y  | __Sticky searching__ allows the developer to start their search in a given string from a custom index other than 0. In other words, the developer can search for matches in the string at any index, such as 2,3 or 5 
u  | __Unicode search__ provides a unique number for every character including punctuation marks, mathematical symbols, technical symbols, arrows, and characters making up non-Latin alphabets such as Thai, Chinese, or Arabic script. So that strings with such characters will be able to be encoded properly. To elaborate, __Unicode Search__ is used in JavaScript for encoding strings. Most characters are encoded with 2 bytes, but that is only able to represent at most 65536 characters. That range is not big enough to encode all possible characters, which is why some rare characters are encoded with 4-bytes, such as 𝒳 (mathematical X) or 😄 (a smile emoji) and some hieroglyphs and so on; without __Unicode__, JavaScript reads 4-byte characters as pairs of 2-bytes, leading to an odd count in the string. But with __Unicode__, that issue is negated since __Unicode__ is able to handle 4-bytes correctly. In short, 

- An example for __Ignore Casing__ would be: 
```
var str = "Hello world! This 'Hello World' convention is quite common in introducing programming languages."; 
var regex = /hello/i; 
var newStr = str.replace(regex, '(Hello)');
```
Output would be: "world! This 'World' convention is quite common in introducing programming languages.".

- An example for __Global Search__ would be:
```
var str = "50 is the half of 50 x 2 that is 80.";
var newStr = str.replace(/50/g, "40");
console.log(newStr);
```
Output would be: "40 is the half of 40 x 2 that is 80.".


- An example for __Dot all__ would be:
```
The first expression /.+/g without the s flag will match every single line in str. The 'quoted' portions shown below represent the matches:

" 'Content flows' \n 'downward and' \n 'downward' "

The second expression /.+/gs with the s flag will make . match every character including \n, which means that the expression will match the whole string str, as shown below:

" 'Content flows\ndownward and\ndownward' "
```

Output would be: Content flows\ndownward and\ndownward. 


- An example for __Multiline mode__ would be:
```
let str = `1st place: Winnie
2nd place: Piglet
3rd place: Eeyore`;

console.log( str.match(/^\d/gm) ); // 1, 2, 3

-------------------------------------------------

let str = `1st place: Winnie
2nd place: Piglet
3rd place: Eeyore`;

console.log( str.match(/^\d/g) ); // 1
```

Output would be: 1, 2, 3 for the first example; 1 for the second example.


- An example for __Sticky searching__ would be:
```
let str = 'let varName = "value"';

let regexp = /\w+/y;

regexp.lastIndex = 3;
alert( regexp.exec(str) ); // null (there's a space at position 3, not a word)

regexp.lastIndex = 4;
alert( regexp.exec(str) ); // varName (word at position 4)
```

Output would be: the 1st alert would be null, since it's on a white space (space between characters); varname would be in the alert since that is what is at the 4th index.
*__(L in the string is index 0)__*


- An example for __Unicode search__ would be to look for Chinese hieroglyphs:
```
let regexp = /\p{sc=Han}/gu; // returns Chinese hieroglyphs

let str = `Hello Привет 你好 123_456`;

alert( str.match(regexp) ); 
```

Output would be: 你,好

-------------------------------------------------

- Another example would be to find characters that denote a currency, such as $, €, ¥.
```
let regexp = /\p{Sc}\d/gu;

let  str = `Prices: $2, €1, ¥9`;

alert( str.match(regexp) ); 
```

Output would be: $2,€1,¥9

- - - -
### Grouping and Capturing

Grouping and Capturing is very useful when needing to *extract information from strings or data* into unified pattern, so that it matches as a complete block, using your preferred programming language.

- ***Grouping*** simply groups up a sequence of regexp tokens into one single unit.
- ***Capturing*** simply put is, whatever is contained within a group is what is captured and likewise saved in memory by that very group.


Symbol  | Description
------------- | -------------
()  | Parentheses create a capturing croup with what ever value is in the parentheses. 
a(__bc__) | The parentheses create a capturing group with value __bc__
<>  | The less than and greater than signs make a group with what ever value is inside. 
```a(?<foo>bc) ```| The "?" disables the capturing group, while ```?<foo>``` was a name that was put into a group.

- - - -
### Bracket Expressions

Bracket expressions are a special kind of character classes. In that they both use ```[]```, ```^```, ```-``` and specify what set or a singular type of character(s) to match. One key difference is that the backlash is NOT a metacharacter 

Symbol  | Description
------------- | -------------
[]  | makes a class that can be used to find a match for one or a set of characters 
[abc] | matches a string that has either an a, ab or ac. The same goes for a|b|c, where it could be ab, b or bc.

- - - -
### Greedy and Lazy Match
*Greedy* means match longest possible string. 

- For every position in the string
    - Try to match the pattern at that position.
    - If there’s no match, go to the next position.

*Lazy* means match shortest possible string.

- repeat minimal number of times
- Enable it by putting a question mark '?' after the quantifier, so that it becomes *? or +? or even ?? for '?'.

Symbol  | Description
------------- | -------------
.+  | greedy
*?, +?, ?, ?? | lazy

- - - -
### Boundaries

Boundaries use the metacharacter ```\b``` which is an anchor like the caret and the dollar sign. It matches at a position that is called a “word boundary”. This match is zero-length.

- A *zero-width* or *zero-length* match is a regular expression match that does not match any characters. It matches only a position in the given string.  

- There are three different positions that qualify as word boundaries:

    - Before the first character in the string, if the first character is a word character.
    - After the last character in the string, if the last character is a word character.
    - Between two characters in the string, where one is a word character and the other is not a word character.

Simply put: ```\b``` allows you to perform a “whole words only” search using a regular expression in the form of ```\b```word```\b```. A “word character” is a character that can be used to form words. All characters that are not “word characters” are “non-word characters”.

Symbol  | Description
------------- | -------------
\b  | wrap this around the word your are looking for, and as long as it is surrounded by other characters then it will be found
\Babc\B | matches only if the pattern is fully surrounded by word characters

- Example: 
```
\Babc\B

"ab abc abcc babcd"
```

Output would be: abc from `babcd`

- - - -
### Back-references

Backreferences match the same text as previously matched by a capturing group.

Symbol  | Description
------------- | -------------
\1  | (backslash one) references the first capturing group. `\1` matches the exact same text that was matched by the first capturing group

- - - -
### Look-ahead and Look-behind

Look-ahead commands to look for `X` but match only when it is followed by `X`. Any pattern can be used instead of `X` and `Y`. While looking for ```X(?=Y)```, the engine of the regular expression detects `X` and then checks whether there is `Y` right after it. In the event that there is no `Y`, then the match is skipped, and the search goes on, but if there is a `Y`, then a match is found and returned.

Lookbehind allows adding a condition for what is behind. In other words, it allows matching a pattern only if there is something before it.

Symbol  | Description
------------- | -------------
(?=) and (?<=)  | operations 
d(?!r)  | matches a d only if is not ***followed*** by r, but r will not be part of the overall regex match
(?<!r)d | matches a d only if is not ***preceded*** by an r, but r will not be part of the overall regex match

## Author

***Christian Casillas*** ~ to see more of my work, please visit my [GitHub](https://github.com/Casres). 