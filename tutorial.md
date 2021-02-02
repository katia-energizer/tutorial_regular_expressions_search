---
type: tutorial
layout: tutorial
title:  "Searching with Regular Expressions"
description: "This tutorial demonstrates how to write patterns with regular expressions and use these patterns for searching in a text."
authors: Andrey Vityuk
date: 2021-02-02
showAuthorInfo: false
---

To get started, you need to create an application [using Intellij IDEA](https://kotlinlang.org/docs/tutorials/jvm-get-started.html) or another IDE with the Kotlin Programming Language support. 

## Create a regular expression

There may be times when you need to use [regular expressions](https://www.regular-expressions.info/quickstart.html). 

Regular expression or regex is a sequence of characters that forms a pattern. This pattern can help you to search certain data in a text. 

The most basic regular expression consists of a single literal character or a sequence of literal characters. 

* `a` matches the first occurrence of the "a" character in your text.
* `apple` matches the first occurrence of the "apple" characters in your text.

More complex regular expressions include special characters. 
* `\s` matches the first occurrence of the white space character in your text.
* `-?\\d+(\\.\\d+)?` matches the first occurrence of the number in your text.

You can compine literal and special characters to can create complex patterns. For the full information about available syntax, see [the Pattern syntax reference for JVM](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html).

### Define the text you plan to search in.

1. Introduce a local variable `text` with the keyword `val`. 
2. Paste the following value to the `text` variable: "Actomyosin, actor, 123.5, actress, 505, actual, actually, actuary"

```
val text = "Actomyosin, actor, 123.5, actress, 505, actual, actually, actuary"
```

We will use a short list of words and numbers as mock data. You can also use the text of your choice. In this case, you will need to configure a search pattern that will be relevant for your text, but you still can refer to the functions and options described in this tutorial.

### Define the the pattern to search with.

1. Introduce a local variable `pattern` with the keyword `val`. 
2. Assign the `actual` value to this variable.

```
val pattern = "actual"
```
3. Now, your pattern is just a text string. To make it into a regular expression, assign the `Regex` type to the value.

```
val pattern = Regex("actual")
```

In this example, we added the `Regex` type to the value. Alternatively, you can use the `toRegex` function.

```
val pattern = "actual".toRegex()
```

## Search with a regular expression

The presence of the `Regex` type allows the compiler to use the following functions for your text:

* [containsMatchIn](#containsMatchIn)
* [find](#find)
* [findAll](#findAll)
* [matchEntire](#matchEntire)
* [matches](#matches)

The `Regex` type also allows to use special [options](#Add_an_option_to_a_regular_expression) with the regular expressions.

Note that the list above is not the full list of functions that are provided by the `Regex` type. For the full list, refer to [the Regex type reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/#kotlin.text.Regex).


### containsMatchIn

The `containsMatchIn` function indicates whether the regular expression can find at least one match in your text.

Define if the pattern has a match in the text.

1. Introduce a local variable `result1` with the keyword `val`. 
2. Assign the following value to the `result1` variable:

```
pattern.containsMatchIn(text)
```
where:
* `pattern` is a variable for the search pattern.
* `containsMatchIn` is a search function.
* `text` is a variable for the text where we are searching for matches.

3. Use the `println` function to display the result of the `result1` variable.

```
val result1 = pattern.containsMatchIn(text)
println(result1)
```
4. To run your application, click the green `Run` icon in the gutter and select `Run 'MainKt'`.

The pattern has matches in the text, so the `containsMatchIn` function returns the `true` value.


### find

The `find` function returns the first match of a regular expression in the text. 

Find the first match of the pattern in the text.

1. Introduce a local variable `result2` with the keyword `val`. 
2. Assign the following value to the `result2` variable: 
 
```
pattern.find(text)
```
where:
* `pattern` is a variable for the search pattern.
* `find` is a search function.
* `text` is a variable for the text where we are searching for matches.

3. Use the `println` function to display the result of the `result2` variable. Use the `range` function to get a range of indexes in the text string. 
4. If the pattern does not contain matches in the text, the `find` function returns null. To allow the `range` function to return null, add a question mark `?` after the `result2` variable name. For information about the danger of null references, refer to [Null Safety](https://kotlinlang.org/docs/reference/null-safety.html).

```
val result2 = pattern.find(text)
println(result2?.range) 
```
5. To run your application, click the green `Run` icon in the gutter and select `Run 'MainKt'`.

The pattern is available in the text, so the `find` function returns the `40..45` range of indexes.

For information about this function parameters and exceptions, refer to [the find function reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/find.html). 

### findAll

The `findAll` returns all matches of the regular expression in your text. 

Find all pattern matches in the text.

1. Introduce a local variable `result3` with the keyword `val`. 
2. Assign the following value to the `result3` variable:

```
pattern.findAll(text)
```
where:
* `pattern` is a variable for search pattern.
* `findAll` is a search function.
* `text` is a variable for the text where we are searching for matches.

3. The result of the `findAll` function is a sequence of values. Use the `forEach` function to display the result as a column of values. For information about this function, refer to [the forEach function reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/for-each.html).

```
val result3 = pattern.findAll(text)
result3.forEach { match ->
   val indexes = match.range
   println("$indexes")
}
```

4. To run your application, click the green `Run` icon in the gutter and select `Run 'MainKt'`.

The pattern has two matches in the text: `actual` and `actual` in `actually`, so the `findAll` function returns 2 values: `40..45` and `48..53`.

For information about function parameters and exceptions, refer to [the findAll function reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/find-all.html).

### matchEntire

The `matchEntire` function attempts to match the regular expression against the entire text string. 

Define if the pattern matches the entire text.

1. Introduce a local variable `result4` with the keyword `val`. 
2. Assign the following value to the `result4` variable: 

```
val result4 = pattern.matchEntire(text)
```

where:
* `pattern` is a variable for search pattern.
* `matchEntire` is a search function.
* `text` is a variable for the text where we are searching for matches.

3. Use the `println` function to display the result of the `result4` variable. Use the `range` function to get a range of indexes in the text string. 
4. If the pattern does not contain matches in the text, the `matchEntire` function returns null. To allow the `range` function to return null, add the question mark `?` after the `result4` variable name. For information about the danger of null references, refer to [Null Safety](https://kotlinlang.org/docs/reference/null-safety.html).

```
val result4 = pattern.matchEntire(text)
println(result4?.range)
```

5. To run your application, click the green `Run` icon in the gutter and select `Run 'MainKt'`.

The pattern does not match the text, so the function returns null.

### matches

The `matches` function indicates whether the regular expression matches the entire text string. 

Define if the pattern has a match in the text.

1. Introduce a local variable `result5` with the keyword `val`. 
2. Assign the following value to the `result5` variable:

```
pattern.matches(text)
```
where:
* `pattern` is a variable for the search pattern.
* `matches` is a search function.
* `text` is a variable for the text where we are searching for matches.

3. Use the `println` function to display the result of the `result5` variable.

```
val result5 = pattern.matches(text)
println(result5)
```
4. To run your application, click the green `Run` icon in the gutter and select `Run 'MainKt'`.

The pattern does not match the text, so the function returns the `false` value.

## Add an option to a regular expression

You can use special options with the regular expression.

In this tutorial, we will cover the `IGNORE_CASE` option. For information about other options, refer to [the RegexOption type reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex-option/).

Add option to a regular expression.

1. Modify the value of the `pattern` variable from `actual` to `Actual`.

```
val pattern = Regex("Actual")
```

2. Click the green `Run` icon in the gutter and select `Run 'MainKt'` to re-run your application.
3. Check results. They have changed. For example, the `find` function result is `false` now. In Kotlin, `Actual` does not equal `actual`, so there are no matches in the text. 
4. Add the `IGNORE_CASE` option to the pattern variable to enable case-insensitive matching:

```
val pattern = Regex("Actual", RegexOption.IGNORE_CASE)
```

5. Click the green `Run` icon in the gutter and select `Run 'MainKt'` to re-run your application. Results for `actual` and `Actual` patterns are the same now.

## What's next?

In this tutorial, we explained how to write patterns with regular expressions and use these patterns for searching data in a text. To extend this knowledge, you can search for a number using the pattern with the special characters or replace data in the text using [other functions of the `Regex` type](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/#kotlin.text.Regex$replace(kotlin.CharSequence,%20kotlin.String)/input).
