# Regex Explanation

TODO:Introductory paragraph (replace this with your text)

# Summary

Today you will read about what a regex, or regular expression is. In short a regular expression is a sequence of character that specifies a search pattern in text. You cna use a regex to narrow down a search, create parameters for usernames and passwords, and clean up information from an api that you may need to use for your app.

This is the snippet of code I will be breaking down for you today. This example will show you how to match an Email: `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

# Table of Contents

- [Regex Components](#regex-components)
- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)
- [Resources](#resources)
- [Author](#author)

# Regex Components

A regex is considered a literal and must be wrapped in forward slash characters (/). If we examine the snippet we are going to break down, `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, you see that it is wrapped in the aforementioned character.

## Basic Elements

- #### . $~~$ Lets you match any single character. An example: po.s will match with pots, pods, and pops.
- #### \ $~~$ Followed by a single character this will let you use special characters without their associated special meaning. Using them this way is called "escaped." Special character examples are asl follows: \ . $ \* ? + [ ] ( ) |

- #### \$ $~~$ Lets you match the end of a string where a pattern occurs. An example: come$ will match come and become but not comedy.

- #### ^ $~~$ Lets you match the beginning of a string where a pattern occurs. An example: come will match comedy but not welcome. An example: $Magician will match with Magician and The Magician but not with magician because regex is case-sensitive.

- #### [ ] $~$ Lets you match any single character in brackets or a range. An example: [aeiou] matches any vowel and if you put a carat in front of it it will match anything that doesn't have a vowel. [^aeiou].

- #### | $~~~$ This indicates an OR operation. An example: keys|socks will find keys or socks.

- #### ( ) $~$ Lets you group expressions. An example: (keys[0-9])|(socks[0-9]) matches keys99a or socks99b but not keys or socks.

- #### A $~~$ This can be any single character or string of characters to be matched. An example: 'e' will match keys in addition you can combine multiple characters like 'keys' to match keys.

## Qualifying Characters

- #### \* $~~~$ Lets you match 0 or other occurrences of the element that come after it. An example: keys*[a-z0-9]\* will match keys_0 and will match additional alphanumeric values. Will also match keys_0, keys_000, keys_zzz, ans keys*.

- #### \+ $~~$ This does the same thing as "\*" but does not match keys\_.

- #### ? $~~~$ Lets you match with 0 or 1 occurrences of the element it follows. An example: keys*[a-a0-9]? matched keys followed by 0 or 1 alphanumeric values. This allows the matching of keys*, keys_0, keys_a, and keys_zz.

# Anchors

Characters ^ and $ are considered anchors.

- [\$](#lets-you-match-the-end-of-a-string-where-a-pattern-occurs-an-example-come-will-match-come-and-become-but-not-comedy) anchor followed by a character or string will match the characters that end a string.
- [^](#lets-you-match-the-beginning-of-a-string-where-a-pattern-occurs-an-example-come-will-match-comedy-but-not-welcome-an-example-magician-will-match-with-magician-and-the-magician-but-not-with-magician-because-regex-is-case-sensitive) anchor followed by a character or string will match with the characters at the beginning of a string.

For example, the snippet we are breaking down, `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, must start with something that matches the pattern [a-z0-9_-] meaning any letter, number, underscore, period, and/or hyphen. It must also end with the pattern [a-z\.] meaning any number and/or period. You can also exclude characters by placing a carat at the beginning of an expression.

# Bracket Expressions

- [\[ \]](#lets-you-match-any-single-character-in-brackets-or-a-range-an-example-aeiou-matches-any-vowel-and-if-you-put-a-carat-in-front-of-it-it-will-match-anything-that-doesnt-have-a-vowel-aeiou) Also known as positive character groups, bracket expressions are anything inside of brackets and can represent any range of characters that we want to match. You will commonly see letter and numbers hyphenated in the brackets annotating that it will search the whole range of number or letters.

For example, in the snippet we are breaking down, `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, the first set of brackets you see "a-z0-9\_\.-" this allows you to match all letter a through z, all numbers 0 through 9, underscores, periods, hyphens. You can also put individual expressions in brackets to match them individually. "Mike.Smith_12-86" would bring back a match, but "$Mike.Smith_12-86" would not match. [^a-za-z] would exclude all letters uppercase and lowercase.

# Quantifiers

Quantifiers set the limits of the string that your regex matches. It can also set limits to parts of the string. They will include the minimum and maximum amount if numbers the regex is looking for.

Quantifiers are inherently "greedy," meaning they match as many occurrences of characters that the regex is looking for. They are included in the following:

- [\*](#lets-you-match-0-or-other-occurrences-of-the-element-that-come-after-it-an-example-keysa-z0-9-will-match-keys0-and-will-match-additional-alphanumeric-values-will-also-match-keys0-keys000-keyszzz-ans-keys) $~~$ Matches the pattern 0 or more times.

- [+](#this-does-the-same-thing-as--but-does-not-match-keys) $~$ Matches the pattern 1 or more times.

- [?](#lets-you-match-with-0-or-1-occurrences-of-the-element-it-follows-an-example-keysa-a0-9-matched-keys-followed-by-0-or-1-alphanumeric-values-this-allows-the-matching-of-keys-keys0-keysa-and-keyszz) $~~$ Matches the pattern 0 or no times.

- { } $~$ Curly brackets can provide can provide three different ways to set limits for a match:

  - {n} $~~~~$ Matches the pattern exactly n number of times.
  - {n,} $~~~$ Matches the pattern at leas n number of times.
  - {n, x} $~$ Matches the pattern from a minimum of n to a maximum of x number of times.

All of the quantifiers can be made lazy by adding the ? symbol after it and will match the fewest number of occurrences possible.

For example, in the snippet of code we are breaking down, `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, you can see at the end {2,6}. This indicates that the suffix of the email address should only be 2-6 characters long.

# Grouping Constructs

- [( )](#lets-you-group-expressions-an-example-keys0-9socks0-9-matches-keys99a-or-socks99b-but-not-keys-or-socks) $~$ The primary way you group a section of a regex is by using parentheses. Each section within parentheses is known as a subexpression.

A grouping constructors have two primary categories: capturing ad non-capturing. A grouping constructor can be made non-capturing simply by adding ?: at the beginning of an expression inside of the parentheses.

For example, in the snippet of code we are breaking down, `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, you can see there are two sets of ( ) in the regex. The first is going to match the prefix of the email address and the sends set is going to match the suffix of the email address.

# Character Classes

A character class in a regex defines a set of characters. All of the character classes can be change to preform the inverse simply by capitalizing the letter. An example: \D will will match any non-digit character.

- . $~~~$ or Any Character: Matches any character except the newline character (\n).

- \d $~$ or Digit: $~~$ Will match all numbers it is equivalent to the expression [0-9].

- \w $~$ or Word: $~~$ Will match all letters, numbers, and underscore. It is equivalent to [A-Za-z0-9-_].

- \s $~~$ or Space: $~~$ Will match any whitespace character, including tabs and line breaks.

# The OR Operator

- [\|](#this-indicates-an-or-operation-an-example-keyssocks-will-find-keys-or-socks) indicates an OR operation.

There is no example in the snippet `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` that have an example of this.

# Flags

I start by explaining that a regex is a literal and must be bound by backslashes. The exception to this rule is know as a flags and they defines additional functions or limits for the regex.

- g $~$ or Global: Makes the expression search for all occurrences.

- i $~~$ or Ignore Casing: Makes the expression search case-insensitively.

- s $~~$ or Dot All: Makes the wild character . match newlines as well.

- m $~$ or Multiline: Makes the boundary character ^ and $ match the beginning and end of every line instead of the beginning and end of the whole string.

- y $~~$ or Sticky: Makes the expression start its search from the index indicated in its "lastIndexed" property.

- u $~~$ or Unicode: Make the expression assume individual characters as code points, not code units, and thus match 32-bit characters as well.

# Character Escapes

- [\\](#followed-by-a-single-character-this-will-let-you-use-special-characters-without-their-associated-special-meaning-using-them-this-way-is-called-escaped-special-character-examples-are-asl-follows) backslash in a regex allows characters to "escape" literal interpretation. This allows you to use "[" so you can match an open bracket instead of using the open bracket functionality and not use a bracket expression.

For example, the snippet of code we are breaking down, `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, in the first set of brackets \. allows the period to be matched and prevents matching the functionality if the period.

# Resources

### Webtrends - https://analytics.webtrends.help/docs/regular-expression-components

### Github Coding Boot Camp https://coding-boot-camp.github.io/full-stack/computer-science/regex-tutorial

# Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
