---
type: tutorial
layout: tutorial
title:  "Searching with Regular Expressions"
description: "This tutorial demonstrates how to write patterns with regular expressions and use these patterns for searching in a text."
authors: Andrey Vityuk
date: 2021-02-03
showAuthorInfo: false
---

This tutorial demonstrates how to write patterns with regular expressions and use these patterns for searching in a text.

You will create a regular expression and write search functions using this regular expression.

This tutorial consists of two parts:

* [Create a regular expression](#Create-a-regular-expression)
* [Search with a regular expression](#Search-with-a-regular-expression)

You will learn about five search functions:

| **Function** | **Description**  |
|---------------|------------------|
| [`containsMatchIn`](#containsMatchIn--finds-out-does-the-text-contain-any-matches)| Finds out does the text contain any matches. |
| [`find`](#find--finds-the-first-match)                                            | Finds the first match. |
| [`findAll`](#findAll--finds-all-matches)                                          | Finds all matches. |
| [`matchEntire`](#matchEntire--finds-out-does-the-regular-expression-match-the-whole-text-returns-a-Booolean-value) | Finds out does the regular expression match the whole text. Returns a Booolean value. |
| [`matches`](#matches--finds-out-does-the-regular-expression-match-the-whole-text-returns-a-parameter) | Finds out does the regular expression match the whole text. Returns a parameter. |

To get started, you need to create an application [using Intellij IDEA](https://kotlinlang.org/docs/tutorials/jvm-get-started.html) or another IDE with the Kotlin Programming Language support. 

## Create a regular expression

There may be times when you need to use [regular expressions](https://www.regular-expressions.info/quickstart.html).

Regular expression or regex is a sequence of characters that forms a pattern. This pattern can help you to search certain data in a text. 

Basic regular expressions consist of a single literal character or a sequence of literal characters. 

* `a` matches the first occurrence of the **a** character in your text.
* `actor` matches the first occurrence of the **actor** character sequence in your text.

More complex regular expressions include special characters. 
* `\s` matches the first occurrence of the white space character in your text.
* `\b[1-9][0-9]{2,4}\b` matches the first occurrence of the number between 100 and 99999 in your text.

You can combine literal and special characters to create complex patterns. For the full information about available syntax, refer to the [Pattern syntax reference for JVM](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html).

### Define the text you plan to search in

1. Introduce a local variable `text` with the keyword `val`. 
2. Assign the following value to the `text` variable: Actomyosin, actor, 123.5, actress, 505, actual, actually, actuary.

   ```kotlin
   val text = "Actomyosin, actor, 123, actress, 505, actual, actually, actuary"
   ```

>
In this tutorial, we will use a list of words and numbers as mock data. You can also use the text of your choice. In this case, you will need to configure a search pattern that will be relevant for your text, but you still can refer to the described functions and options.
>

### Define the pattern to search with

1. Introduce a local variable `pattern` with the keyword `val`. 
2. Assign the `\b[1-9][0-9]{2,4}\b` value to this variable.

   ```kotlin
   val pattern = "\b[1-9][0-9]{2,4}\b"
   ```

This regular expression will match numbers in your text.

3. Add extra backslash before each `\b` part of the regular expression. `\b` is a metacharacter with a special meaning: it matches a number boundary. You must use `\` as an escape character before metacharacters. Otherwise metacharacters will be read by compiler literally without any special meanings. 

   ```kotlin
   val pattern = "\\b[1-9][0-9]{2,4}\\b"
   ```

3. For now, your pattern is just a text string. To make it into a regular expression, assign the `Regex` type to the value.

   ```kotlin
   val pattern = Regex("\\b[1-9][0-9]{2,4}\\b")
   ```

In this example, we added the `Regex` type to the value. Alternatively, you can use the `toRegex` function.

   ```kotlin
   val pattern = "\\b[1-9][0-9]{2,4}\\b".toRegex()
   ```

>
In this tutorial, we will search for numbers. You can also create a regular expression of your choice. In this case, you will need to have a relevant text for your regular expression, but you still can refer to the described functions and options.
>

## Search with a regular expression

In this part, you will learn how to:

* Find out does the text contain any matches of your regular expression ([`containsMatchIn`](#containsMatchIn--finds-out-does-the-text-contain-any-matches))
* Find the first regular expression match in the text ([`find`](#find--finds-the-first-match))
* Find all regular expression matches in the text ([`findAll`](#findAll--finds-all-matches))
* Find out does your regular expression match the whole text; depending on a applied function, you can get a Boolean value ([`matchEntire`](#matchEntire--finds-out-does-the-regular-expression-match-the-whole-text-returns-a-Booolean-value)) or a certain match parameter ([`matches`](#matches--finds-out-does-the-regular-expression-match-the-whole-text-returns-a-parameter)).

You can find the full list of functions in the [`Regex` type reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/#kotlin.text.Regex).

### containsMatchIn — finds out does the text contain any matches 

The `containsMatchIn` function attempts to can find a match of the regular expression in your text.

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

```kotlin
fun main() {

   val text = "Actomyosin, actor, 123, actress, 505, actual, actually, actuary"
   val pattern = Regex("\b[1-9][0-9]{2,4}\b")
   val result1 = pattern.containsMatchIn(text)
   
   println("The containsMatchIn function returns $result1.") //true

}
```
   
4. To run your application, click the green **Run** icon in the gutter and select **Run 'MainKt'**.

The pattern has matches in the text, so the `containsMatchIn` function returns the `true` value.

### find — finds the first match

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
4. If the pattern does not have matches in the text, the `find` function returns `null`. To allow the `range` function to return `null`, add a question mark `?` after the `result2` variable name. For information about the danger of null references, refer to [Null Safety](https://kotlinlang.org/docs/reference/null-safety.html).

```kotlin
fun main() {

   val text = "Actomyosin, actor, 123, actress, 505, actual, actually, actuary"
   val pattern = Regex("\b[1-9][0-9]{2,4}\b")
   val result2 = pattern.find(text)
   
   println("The find function returns $result2?.range.") //19..21
   
}
 ```
   
5. To run your application, click the green **Run** icon in the gutter and select **Run 'MainKt'**.

The pattern is available in the text, so the `find` function returns the `19..21` range of indexes.

For information about function parameters and exceptions, refer to the [`find` function reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/find.html). 

### findAll — finds all matches

The `findAll` returns all matches of the regular expression in your text. 

Find all pattern matches in the text.

1. Introduce a local variable `result3` with the keyword `val`. 
2. Assign the following value to the `result3` variable:

   ```
   pattern.findAll(text)
   ```

   where:
   * `pattern` is a variable for the search pattern.
   * `findAll` is a search function.
   * `text` is a variable for the text where we are searching for matches.

3. The result of the `findAll` function is a sequence of values. Use the `forEach` function to display the result as a column of values. For information about this function, refer to the [`forEach` function reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/for-each.html).

```kotlin
fun main() {

    val text = "Actomyosin, actor, 123.5, actress, 505, actual, actually, actuary"
    val just_string = "actual"
   val pattern = Regex("\\b[1-9][0-9]{2,4}\\b")
   
   println("$indexes")
   
}
```

4. To run your application, click the green **Run** icon in the gutter and select **Run 'MainKt'**.

The pattern has two matches in the text: `actual` and `actual` in `actually`, so the `findAll` function returns 2 values: `40..45` and `48..53`.

For information about function parameters and exceptions, refer to the [`findAll` function reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/find-all.html).

### matchEntire — finds out does the regular expression match the whole text; returns a Booolean value

The `matchEntire` function attempts to match the regular expression against the entire text string. 

Define if the pattern matches the entire text.

1. Introduce a local variable `result4` with the keyword `val`. 
2. Assign the following value to the `result4` variable:

   ```
   pattern.matchEntire(text)
   ```

   where:
   * `pattern` is a variable for the search pattern.
   * `matchEntire` is a search function.
   * `text` is a variable for the text where we are searching for matches.

3. Use the `println` function to display the result of the `result4` variable. Use the `range` function to get a range of indexes in the text string. 
4. If the pattern does not have matches in the text, the `matchEntire` function returns `null`. To allow the `range` function to return `null`, add the question mark `?` after the `result4` variable name. For information about the danger of null references, refer to [Null Safety](https://kotlinlang.org/docs/reference/null-safety.html).

   ```kotlin
   val result4 = pattern.matchEntire(text)
   println(result4?.range)
   ```

5. To run your application, click the green **Run** icon in the gutter and select **Run 'MainKt'**.

The pattern does not match the text, so the function returns `null`.

### matches — finds out does the regular expression match the whole text; returns a parameter

The `matches` function indicates whether the regular expression matches the entire text string. 

Define if the pattern matches the entire text.

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

   ```kotlin
    val result5 = pattern.matches(text)
    println(result5)
    ```
    
4. To run your application, click the green **Run** icon in the gutter and select **Run 'MainKt'**.

The pattern does not match the text, so the function returns the `false` value.

## What's next?

In this tutorial, we explained how to write patterns with regular expressions and use these patterns for searching data in a text. To extend this knowledge, you can search for a number using the pattern with special characters or replace data in the text using [other functions of the `Regex` type](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/#kotlin.text.Regex$replace(kotlin.CharSequence,%20kotlin.String)/input).
