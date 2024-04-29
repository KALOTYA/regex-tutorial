# Credit Card Regex

In this tutorial, we will explore how to create a regular expression to validate credit card numbers. We'll cover the components of the regex and explain each part.

## Summary

We will describe a regular expression to validate various credit card number patterns. The regex will support common credit card issuers such as Visa, MasterCard, American Express, Discover, and others. Here is the regex we will be explaining:

```javascript
const creditCardRegex = /^(?:4[0-9]{12}(?:[0-9]{3})?|5[1-5][0-9]{14}|6(?:011|5[0-9][0-9])[0-9]{12}|3[47][0-9]{13}|3(?:0[0-5]|[68][0-9])[0-9]{11}|(?:2131|1800|35\d{3})\d{11})$/;
```

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Author](#author)


## Regex Components

### Anchors
An anchor in regular expressions specifies a position in the string where the match must occur. Anchors do not match any characters themselves but define where in the string the pattern should start or end. Common anchors include ^, which matches the beginning of a line, and $, which matches the end of a line.
```javascript
const creditCardRegex = /^(?:4[0-9]{12}(?:[0-9]{3})?|5[1-5][0-9]{14}|6(?:011|5[0-9][0-9])[0-9]{12}|3[47][0-9]{13}|3(?:0[0-5]|[68][0-9])[0-9]{11}|(?:2131|1800|35\d{3})\d{11})$/;
```
In this regex, "^" ensures that the match starts at the beginning of the string, and "$" ensures that the match ends at the end of the string. This ensures that the entire credit card number is validated, not just a part of it.

### Quantifiers
Quantifiers in regular expressions specify the quantity or repetition of characters or groups in the pattern. They indicate how many times a particular character or group should occur.

Common quantifiers include:
- `*` : Matches zero or more occurrences of the preceding element.
- `+` : Matches one or more occurrences of the preceding element.
- `?` : Matches zero or one occurrence of the preceding element.
- `{n}` : Matches exactly n occurrences of the preceding element.
- `{n,}` : Matches at least n occurrences of the preceding element.
- `{n,m}` : Matches between n and m occurrences of the preceding element.

In the context of the credit card regex, quantifiers are used to specify the length of the credit card numbers. Here's an example:
```javascript
const creditCardRegex = /^(?:4[0-9]{12}(?:[0-9]{3})?|5[1-5][0-9]{14}|6(?:011|5[0-9][0-9])[0-9]{12}|3[47][0-9]{13}|3(?:0[0-5]|[68][0-9])[0-9]{11}|(?:2131|1800|35\d{3})\d{11})$/;
```
In this regex:
- `{12}` : specifies that there must be exactly 12 digits for Visa and MasterCard.
- `{14}` : specifies that there must be exactly 14 digits for some MasterCard numbers.
- `{13}` : specifies that there must be exactly 13 digits for Visa and Discover.
- `{11}` : specifies that there must be exactly 11 digits for American Express and Diners Club.

### Grouping Constructs
Grouping constructs in regular expressions allow you to group parts of the pattern together. They are defined by enclosing expressions within parentheses `()`.

Grouping serves several purposes:
1. Applying Quantifiers: You can apply quantifiers to a group, causing the pattern inside the group to be matched a certain number of times.
2. Capturing: By default, groups capture the matched text so that you can extract it or refer to it later.
3. Alternation: Groups can be used to define alternatives using the `|` operator.

In this regex, grouping constructs `(?: ... )` are used to group different card number patterns together. For example:
- `(?:4[0-9]{12}(?:[0-9]{3})?)` : This group matches Visa card numbers, where the first digit is 4, and the total length is 13 or 16 digits.
- `(?:5[1-5][0-9]{14})` : This group matches MasterCard card numbers, where the first digit is 5 and the total length is 16 digits.
- `(...|...)` : Alternation is used to define different card number patterns separated by the | operator.


### Bracket Expressions
Bracket expressions, also known as character classes, are used to match any single character from a specified set. They are denoted by square brackets `[]` and can contain a list of characters, character ranges, or predefined character classes.

For Example:
- `[abc]` : Matches any of the characters 'a', 'b', or 'c'.
- `[0-9]` : Matches any digit from 0 to 9.
- `[^abc]` : Matches any character except 'a', 'b', or 'c'.
- `[a-zA-Z]` : Matches any uppercase or lowercase letter.

In this Credit Card regex, bracket expressions like [0-9] are used to match any digit. For example:
- [0-9]{12} matches exactly 12 digits in various parts of the regex, such as Visa, MasterCard, and Discover card numbers.
- [47] matches either 4 or 7 in the regex parts that handle American Express and Diners Club card numbers.


### Character Classes

Character classes in regular expressions are predefined sets of characters that match specific types of characters. They are denoted by backslashes followed by a letter or sequence inside square brackets `\` or `[]`. Some common character classes include:
- `\d` : Matches any digit (equivalent to [0-9]).
- `\w` : Matches any word character (letters, digits, or underscores).
- `\s` : Matches any whitespace character (spaces, tabs, newlines).
- `\D` : Matches any non-digit character (equivalent to [^0-9]).
- `\W` : Matches any non-word character.
- `\S` : Matches any non-whitespace character.

In the credit card regex, different ranges of digits are used to identify the first digit of various card issuer networks. For example:
- `[4]` : Matches the first digit of Visa card numbers.
- `[5]` : Matches the first digit of MasterCard card numbers.
- `[3]` : Matches the first digit of American Express and Diners Club card numbers.

### The OR Operator
The OR operator in regular expressions is denoted by the vertical bar `|`. It is used to specify alternatives within the pattern, allowing the regex engine to match any of the alternatives.
For Example:
- `cat|dog` matches either "cat" or "dog".
- `apple|banana|orange` matches either "apple", "banana", or "orange".

In the context of the credit card regex, the OR operator is used to define different patterns for different card issuers. Here's an example:
- `4[0-9]{12}` : Matches Visa card numbers starting with "4".
- `5[1-5][0-9]{14}` : Matches MasterCard card numbers starting with "5".
- `6(?:011|5[0-9][0-9])[0-9]{12}` : Matches Discover card numbers starting with "6".
- `3[47][0-9]{13}` : Matches American Express card numbers starting with "34" or "37".
- `3(?:0[0-5]|[68][0-9])[0-9]{11}` : Matches Diners Club card numbers starting with "300" to "305" or "36" or "38".
- `(?:2131|1800|35\d{3})\d{11}` : Matches JCB card numbers starting with "2131", "1800", or "35".

## Author

Hello! I am Ajay, I am a Web Developer with expertise in Full-Stack Web Development. You can find more of my work on my GitHub profile: [KALOTYA](https://github.com/KALOTYA).
