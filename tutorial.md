---
type: tutorial
layout: tutorial
title:  "Searching with Regular Expressions"
description: "This tutorial demonstrates how to use regular expressions for searching in a text. "
authors: Andrey Vityuk
date: 2021-02-02
showAuthorInfo: false
---

This tutorial demonstrates how to write patterns with regular expressions and use these patterns for searching in a text.

To get started, you need to create an application [using Intellij IDEA](https://kotlinlang.org/docs/tutorials/jvm-get-started.html) or another IDE with the Kotlin Programming Language support. 

## Create a regular expression

There may be times when you need to use [regular expressions](https://www.regular-expressions.info/quickstart.html). 

Regular expression is a character or a sequence of characters that forms a pattern. 
This pattern can help you in matching, parsing, and filtering of a text. 

The most basic regular expression consists of a single literal character.

a
Matches the first occurrence of the “a” character in your text.
1
Matches the first occurrence of the “1” character in your text.
 
Regular expression more likely to consist of a sequence of characters.

apple
Matches the first occurrence of the “apple” characters in your text.
812a
Matches the first occurrence of the “812a” characters in your text.

Regular expressions can also include special characters. Special characters have a special meaning.

\s
Matches the first occurrence of the white space character in your text.
[a-c]
Matches the first occurrence of the character from the range a to d in your text.

Using literal and special characters, you can create complex patterns.

[A-Za-z0-9]
Matches the first occurrence of the alphanumeric character in your text.
-?\\d+(\\.\\d+)?
Matches the first occurrence of the number in your text.

For pattern syntax reference for JVM see https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html 
Define the text you plan to search in.
Introduce a local variable text with the keyword val. 
Paste the following value to the text variable: "Actomyosin, actor, 123.5, actress, 505, actual, actually, actuary"
val text = "Actomyosin, actor, 123.5, actress, 505, actual, actually, actuary"

We will use a short list of words and numbers as mock data. You can also use the text of your choice. In this case, you will need to configure a search pattern that will be relevant for your text, but you still can refer to the functions and options described in this tutorial.

Define the pattern to search with.
Introduce a local variable pattern with the keyword val. 
Assign the actual value to this variable.

val pattern = "actual"

Now, your pattern is just a text string. To make it into a regular expression, assign the Regex type to the value.

val pattern = Regex("actual")

In this example, we added the Regex type to the value. Alternatively, you can use the toRegex function.

val pattern = "actual".toRegex()

Search with a regular expression
The presence of the Regex type allows the compiler to use the following functions for your text:
containsMatchIn
find
findAll
matchEntire
matches

Note that the list above is not the full list of functions that are provided by the Regex type. For the full list, refer to the Regex type reference.
containsMatchIn
The containsMatchIn function indicates whether the regular expression can find at least one match in your text.

Define if the pattern has a match in the text.

Introduce a local variable result1 with the keyword val. 
Assign the following value to the result1 variable:
pattern.containsMatchIn(text)
where:
pattern is a variable for the search pattern.
containsMatchIn is a search function.
text is a variable for the text where we are searching for matches.
Use the println function to display the result of the result1 variable.

val result1 = pattern.containsMatchIn(text)
println(result1) 

To run your application, click the green Run icon in the gutter and select Run 'MainKt'.

The pattern has matches in the text, so the containsMatchIn function returns the true value.
find
The find function returns the first match of a regular expression in the input. 

Find the first match of the pattern in the text.

Introduce a local variable result2 with the keyword val. 
Assign the following value to the result2 variable: 
pattern.find(text)
where:
pattern is a variable for the search pattern.
find is a search function.
text is a variable for the text where we are searching for matches.
Use the println function to display the result of the result2 variable. Use the range function to get a range of indexes in the text string. 
If the pattern does not contain matches in the text, the fund function returns null. To allow the range function to return null, add ? to the result2 variable. For information about the danger of null references, refer to Null Safety.

val result2 = pattern.find(text)
println(result2?.range) 

To run your application, click the green Run icon in the gutter and select Run 'MainKt'.

The pattern is available in the text, so the find function returns the 40..45 range of indexes.

For information about function parameters and exceptions, refer to the find function reference. 
findAll
The findAll function indicates whether the regular expression can find at least one match in your text. 

Find all pattern matches in the text.

Introduce a local variable result3 with the keyword val. 
Assign the following value to the result3 variable:
pattern.findAll(text)
where:
pattern is a variable for search pattern.
findAll is a search function.
text is a variable for the text where we are searching for matches.
The result of the findAll function is a sequence of values. Use the forEach function to display the result as a column of values. For information about this function, refer to the forEach function reference.

val result3 = pattern.findAll(text)
result3.forEach { match ->
   val indexes = match.range
   println("$indexes")
}

To run your application, click the green Run icon in the gutter and select Run 'MainKt'.

The pattern has two matches in the text: actual and actual in actually, so the findAll function returns the 2 values: 40..45 and 48..53.

For information about function parameters and exceptions, refer to the findAll function reference.
matchEntire
The matchEntire function attempts to match the regular expression against the entire text string. 

Define if the pattern matches the entire text.

Introduce a local variable result4 with the keyword val. 
Assign the following value to the result4 variable: 
val result4 = pattern.matchEntire(text)
where:
pattern is the variable for search pattern.
matchEntire is the search function.
text is the variable for the text where we are searching for matches.
Use the println function to display the result of the result4 variable. Use the range function to get a range of indexes in the text string. 
If the pattern does not contain matches in the text, the fund function returns null. To allow the range function to return null, add ? to the result4 variable. For information about the danger of null references, refer to Null Safety.

val result4 = pattern.matchEntire(text)
println(result4?.range)

To run your application, click the green Run icon in the gutter and select Run 'MainKt'.

The pattern does not match the text, so the function returns null.
matches
The matches function indicates whether the regular expression matches the entire text string. 

Define if the pattern has a match in the text.

Introduce a local variable result5 with the keyword val. 
Assign the following value to the result5 variable:
pattern.matches(text)
where:
pattern is the variable for the search pattern.
matches is the search function.
text is the variable for the text where we are searching for matches.
Use the println function to display the result of the result5 variable.

val result5 = pattern.matches(text)
println(result5)

To run your application, click the green Run icon in the gutter and select Run 'MainKt'.

The pattern does not match the text, so the function returns the false value.
Add an option to a pattern

You can use special options with the regular expression.
In this tutorial, we will cover the IGNORE_CASE option. For information about other options, refer to the RegexOption type reference.

Modify the value of the pattern variable from actual to Actual.
Click the green Run icon in the gutter and select Run 'MainKt' to re-run your application.
Check results. Results have changed. For example, the find function result is false now.  Actual does not equal actual in Kotlin, so there are no matches in the text. 
Add the IGNORE_CASE option to the pattern variable to enable case-insensitive matching:
val pattern = Regex("Actual", RegexOption.IGNORE_CASE)
Click the green Run icon in the gutter and select Run 'MainKt' to re-run your application. Results for actual and Actual patterns are the same now.

What's next?
In this tutorial, we explained how to write patterns with regular expressions and use these patterns for searching data in a text. To extend this knowledge, you can search for a number using the pattern with the special characters or replace data in the text using other functions of the Regex type.

