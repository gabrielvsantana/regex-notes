# $ regex-notes

![img](regex-notes.png)

`/<your-regex>/<your-flag>`

<br/>

# Table of Contents

1. [Basic Matchers](#basic-matchers)
1. [Anchors](#anchors)
1. [Quantifiers and Alternation | Repetition](#quantifiers-and-alternation--repetition)
1. [Group & References](#group--references)
1. [Characters Classes](#characters-classes)
1. [Lookarounds](#lookarounds)
1. [Flags (also called modifiers)](#flags-also-called-modifiers)
1. [Especial Characters](#especial-characters)
1. [Greedy Matching vs Lazy Matching](#greedy-matching-vs-lazy-matching)
    1. [Greedy Matching](#greedy-matching)
    1. [Lazy Matching](#lazy-matching)
1. [Word Boundary](#word-boundary)
1. [General examples](#general-examples)
1. [Testing Regex in the command line JavaScript](#testing-regex-in-the-command-line-javascript)

<br/>

# Basic Matchers

`.` - any character

`[abc]` - can be any of the characters inside of the brackets

`[^abc]` - negate the characters

`[a-z]` - letter range

`[0-9]` - number range

## e.g.

bar ber bir bor bur

`/b[aeiou]r/g` = bar ber bir bor bur

`/b[^eo]/g` = bar bir bur

<br/>

# Anchors

`^` - caret sign: It selects chars at the beginning of a line

`$` - dollar sign: It selects chars at the end of a line

`\b` - Word Boundary - Matches the word character or position at the end of a word

`\b` - Not Word Boundary - Matches a word character or position that is not at the end of a word

<br/>

# Quantifiers and Alternation | Repetition

`*` - indicates a char doesn't match or can match many times.

`+` - indicates a char matches one or more times

`?` - indicates a char is optional

`{x}` - indicates a certain number of occurrences of a char

`{x,}` - indicates at least a certain number of occurrences of a char

`{x,y}` - express the occurrence of a char in a certain number range

`|` - pipe character

## e.g.

ber beer beeer beeeer

`/be*r/g` = br ber beer

`/be+r/g` = ber beer

`/colou?r/g` = color colour

`/be{2}r/g` = beer

`/be{3,}r/g` = beeer beeeer

`/be{1,3}r/g` = ber beer beeer 

`/[0-9]{4}/g` = 2021

<br/>

# Group & References

`()` - groups an expression together

`\1` - references the first group to avoid rewriting

`(?:)` - groups an expression together without allowing it to be captured by reference

<br/>

# Characters Classes

`[abc]` - Character Set - can be any of the characters inside of the brackets

`[^abc]` - Not Character Set - negate the characters

`[a-z]` - Range - letter range

`.` - Dot - any character

`\w` - Word - alphanumeric - It selects letters, numbers and underscore chars

`\W` - Not Word - It selects everything besides letters, numbers and underscore chars

`\d` - Digit - It selects only number characters

`\D` - Not Digit - It selects non-numeric characters

`\s` - Whitespace - It selects space characters

`\S` - Not Whitespace - It selects non-space characters

<br/>

# Lookarounds

`(?=)` - Positive Lookahead

`(?!)` - Negative Lookahead

`(?<=)` - Positive Lookbehind

`(?<!)` - Negative Lookbehind

## e.g.

Date: 4 Aug 3 PM

`/\d+(?=PM)/g` = 3

`/\d+(?!=PM)/g` = 4

Product Code: 1064 Price: $5

`/(?<=\$)\d+/ g` = 5

`/(?<!\$)\d+/g` = 1064

<br/>

# Flags (also called modifiers)

`//g` - global - It causes the expression to select all matches. If not used it will only select the first match.

`//m` - multiline - RegEx sees all text as one line. We use the multiline flag to handle each line separately.

`//i` - case insensitive - To remove the case-sensitiveness of the expression we write, we must activate this flag.

<br/>

# Especial Characters

`|` - pipe character - conditional - I love (cats|dogs)

`\` - escape character - We need to use before selecting a special character

<br/>

# Greedy Matching vs Lazy Matching

ber beer beeer beeeer

## Greedy Matching

RegEx does a greedy match by default. It refers to any match that ends with "r" but it doesn't stop at the first letter.

`/.*r/` = ber beer beeer beeeer

It refers to any match that ends with "r" but it doesn't stop at the first letter.

## Lazy Matching

Unlike Greedy Matching it stops at the first matching.

`/.*?r/` = ber

<br/>

# Word Boundary

`\b` - Word Boundary - Matches the word character or position at the end of a word

`\B` - Not Word Boundary - Matches a word character or position that is not at the end of a word

`/n\b/` = aN answer or a questioN

`/n\B/` = an aNswer or a question

<br/>

# General examples

ha-ha,haa-haa

`/(haa)/g` = haa haa

`/(ha)-\1,(haa)-\2/g` = ha-ha,haa-haa

`/(?:ha)-ha,(haa)-\1/g` = ha-ha,haa-haa

`/(C|c)at|rat/g` = cat Cat rat

`/(\*|\.)/g` = * .

`/^[0-9]/gm` = It selects only the number at the beginning of a line

`/html$/g` = 

`/\w/g` = 

<br/>

# Testing Regex in the command line JavaScript

```ts
/<your-regex>/.test(<your-string>)
```

I would recommend using the execute method which returns null if no match exists otherwise it returns a helpful object.

```ts
let case1 = /^([a-z0-9]{5,})$/.exec("abc1");
console.log(case1); //null
```

```ts
let case2 = /^([a-z0-9]{5,})$/.exec("pass3434");
console.log(case2); // ['pass3434', 'pass3434', index:0, input:'pass3434', groups: undefined]
```
