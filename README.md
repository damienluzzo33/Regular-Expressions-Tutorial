# Regular Expressions Tutorial

Welcome to the Regular Expressions Tutorial. In this tutorial, I will walk you through the most comprehensive introductory walk-through on regular expressions on GitHub!

## Summary

In this tutorial, I will explain how you can use regular expressions to validate a proper email input. We will use this RegEx to ensure that a given email, potentially submitted by a user in your application, is a valid email address. In the end, you'll fully understand the power of regular expressions, and you'll walk away with the perfect expression that you can use to validate any email.

Our regular expression will look like the following:

```
^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$
```

This may look complicated at first, but in due time, it will make perfect sense how we can use the above expression to make sure that a user's email address matches the pattern we are aiming to validate.

While this intro will cover the basics of regular expressions to "validate" something, you can also use RegEx to "extract" pieces of a string that matches the pattern you create, "substitute" pieces of strings with other strings, and "split" pieces of the pattern you specify to convert the string to an array of pieces of that string (similar to what the split method does to strings in Javascript).

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components
There are many RegEx components at our disposal when using regular expressions. The main components we use in RegEx are "Single Characters", "Wildcards", "Brackets Expressions", "Escaped Characters", "Groups", and "Quantifiers". The following sections will outline everything you need to know.

When writing general expressions, we don't want any spaces in our expression. And we want to begin and end our expression with a "/". In the example we will be using, we'll be using Javascript.

### Anchors
Anchors are used to tell RegEx what you are doing with a specified component. We can us "^" to denoted the beginning of our RegEx and "$" to denote the end. 

For our email example, we want to start our RegEx with a speific component. Let's practice this thought process with the email: example123@email.com. Here we can see that we have "example123", then "@", then "gmail", then ".", and finally, "com". So, we want to start the expression with "example123" and we want to end it with "com".

Our code will start as something like this: 
```
/^
```
And our code with end with something like this: 
```
$/
```

While they are not as common, you can also use /b and /B. /b will allow you to see if the user's input has something specific at the start/end of string (before or after a space). 

### Character Classes
Character classes allow us to specify the characters that we are looking for from a user's response. 

There are tons of character classes, including: "[xyz]" which will match any character specified in the set, "[^abc]" which will match any character that is NOT specified in the set, "[a-z]" which will match any character that is specified in the range provided in the set, "." allows us to match any character (besides line-breaks), [\s\S] which allows us to match anything (including line-breaks), "\w" or "\W" which respectively allow us to match every word or everything that isn't a word, and "/d" or "/D" which respectively allow us to match every digit or everything that isn't a digit from the user;s input. 

### Bracket Expressions
Bracket expressions allow us to match any characters or ranges of characters that we wish. We can write bracket expressions to include lowercase letters, uppercase letters, numbers, and special characters.

In the beginning of our email example, remember that we want to match "example123" after the "^" anchor. We can do this with a character set by allowing all letters and numbers in our brackets. 

Our updated beginning now looks like this: 
```
/^[a-zA-Z0-9_]
```

We've got some more work to do, but now our users can enter emails that start with any character from lowercase letters "a-z", capital letters "A-Z", numbers "0-9", and underscores.

The middle part of our example, between the "@" and the "." is the email provider. This can be anything, like the beginning can. So we write it the same way but without the carrot "^" because this part will not be at the beginning. 
```
[a-zA-Z0-9_]
```

Finally, our ending portion will be something like "com", "io", or "net", so we are only worried about allowing alphabetic characters for the user's email submission. Now we can bring in the "$" to signify the end.

The ending of our expression will look like this: 
```
[a-zA-Z]$/
```

### Character Escapes
Character escapes allow us "escape" keywords and special characters in RegEx and use them in of our expression to match the character they represent on the keyboard. There are quite a few escape characters in RegEx, but the most commonly used is the "\" which, when it comes before something, let's us access the character as a pattern match parameter in our regular expressions.

For our example, we want to allow users to include a "-" and a "." in the first part of their email submission. So, we need to use the escape character "\" to make those match parameters available to us.

Our updated expression beginning should now be: 
```
/^[a-zA-Z0-9_\-\.]
```
Our updated expression beginning should now be: 
```
[a-zA-Z0-9_\-\.]
```
Our ending will look the same: 
```
[a-zA-Z]$/
```

### Quantifiers
Quantifiers are the pieces of RegEx that allow us to specify the amount of a component we are using to validate a user's input. "+" means one or more of the thing that preceded the plus sign, "*" means 0 or more, "?" means that the thing is optional, and {min, max} allows us to specify the min and max quantity of something that we are expecting.

In our example, the way our expression stands now, it will only recognize the first letter in the example email. But we want to allow the user to add as many of the allowed characters as they want to before the "@" in "example123@email.com". To do this, we just need to add a "+" to that part of the expression.

Our updated expression beginning will look like this: 
```
/^[a-zA-Z0-9_\-\.]+
```
Our updated expression middle will look like this: 
```
[a-zA-Z0-9_\-\.]+
```
Our ending expression will change this time. We need to understand first that endings of emails end in 2, 3, 4, or 5 characters, so we specify a "{min, max}" range for that portion's character length: 
```
[a-zA-Z]{2,5}$/
```

### Grouping Constructs
Grouping Constructs allow us to "group" parts of an overall expression. This gives us the ability to group together multiple components to match something that meets that grouped construct. To group a section of an expression to be evaluated as an individual piece of the expression, we use "(xyz)". 

In our example, we have three separate pieces that need to come together and make validation determinations based on each piece we've constructed. To do this, we put them into their own group using grouping constructs. 

Our expression beginning should look like this: 
```
/^([a-zA-Z0-9_\-\.]+)
```
Our expression middle will look like this: 
```
([a-zA-Z0-9_\-\.]+)
```
Our ending expression piece will be: 
```
([a-zA-Z]{2,5})$/
```

Since we already know how to escape special characters with "/", we can use to match "." and, along with "@" which is not a reserved character, we can now piece our entire regular expression together as follows: 

```
/^([a-zA-Z0-9_\-\.]+)@([a-zA-Z0-9_\-\.]+)\.([a-zA-Z]{2,5})$/
```

### The OR Operator
The OR Operator gives us the ability to create a logical OR operation to say that we are expecting one thing OR another in our regular expression. To use the logical OR, we simply use "|". We can also chain together as many logical OR operators that we want to.

In our example, we could allow the user to enter a phone number instead of an email. Assume we have a very user-choice driven application that allows this type of input. To implement this, we need to create the RegEx that can validate a proper phone number. 

Let's make a basic RegEx that can match something like "123-456-7890". To do this, we first need to start with a "^" and then allow any number one through nine with "[1-9]" or "/d" for the first three digit "{3}".

Next, we'll do the same thing for the middle three numbers without the carrot. And finally, we'll do the same thing with four digits to end the expression along with a "$". We will also have to connect these expression pieces together with dashes by escaping it's reserved character nature with "/-".

Our phone number RegEx will look like this: 
```
^\d{3}-\d{3}-\d{4}$
```

To put this all together, we wrap each of our final expressions in grouping constructs and place the OR operator between them to create one massive regular expression that will give our user a choice of entering a valid email or a valid phone number of the format "XXX-XXX-XXXX".

Our final regular expression will look like this: 
```
/(^([a-zA-Z0-9_\-\.]+)@([a-zA-Z0-9_\-\.]+)\.([a-zA-Z]{2,5})$)|(^\d{3}-\d{3}-\d{4}$)/
```

### Flags
Flags are special characters that we can add to the end of an expression, after the "/" to denote how the RegEx as a whole should be interpreted. Here's the most common: "i" tells the RegEx to not be case-sensitive, "g" lets you search through every matching result your regular expression matches, and "m" which allows the "^" and "$" to refer to the start and end of a line instead of a string.

There is no special need in our example to use any flag in particular, but they will become useful to you one day.

## Author

