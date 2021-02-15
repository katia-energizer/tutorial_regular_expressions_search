---
type: tutorial
layout: tutorial
title:  "Searching with Regular Expressions"
description: "This tutorial demonstrates how to write patterns with regular expressions and use these patterns for searching in a text."
authors: Andrey Vityuk
date: 2021-02-03
showAuthorInfo: false
---

You will create search patterns with a regular expression and write search functions using these patterns.

This tutorial consists of two parts:

* [Create a pattern with a regular expression](#Create-a-pattern-with-a-regular-expression)
* [Search with a pattern](#Search-with-a-pattern)

   In the second part, you will learn about five search functions:

   | **Function** | **Description**  |
   |---------------|------------------|
   | [`containsMatchIn`](#containsMatchIn--finds-out-if-the-text-contains-any-matches)| Finds out if the text contains any matches. |
   | [`find`](#find--finds-the-first-match)                                            | Finds the first match. |
   | [`findAll`](#findAll--finds-all-matches)                                          | Finds all matches. |
   | [`matchEntire`](#matchentire--finds-out-if-the-pattern-matches-the-whole-text-returns-a-match-parameter) | Finds out if the pattern matches the whole text. Returns a match parameter. |
   | [`matches`](#matches--finds-out-if-the-pattern-matches-the-whole-text-returns-a-Boolean-value) | Finds out if the pattern matches the whole text. Returns a Boolean value. |

To get started, you need to create an application [using Intellij IDEA](https://kotlinlang.org/docs/tutorials/jvm-get-started.html) or another IDE with the Kotlin Programming Language support. 

## Create a pattern with a regular expression

There may be times when you need to use [regular expressions](https://www.regular-expressions.info/quickstart.html).

Regular expression or regex is a sequence of characters that forms a pattern. This pattern can help you to search certain data in a text. 

Basic regular expressions consist of a single literal character or a sequence of literal characters. 

* `a` matches the first occurrence of the **a** character in your text.
* `actor` matches the first occurrence of the **actor** character sequence in your text.

More complex regular expressions include special characters. 
* `\s` matches the first occurrence of the white space character in your text.
* `\b[1-9][0-9]{2}\b` matches the first occurrence of the number between 100 and 999 in your text.

You can combine literal and special characters to create complex patterns. For the full information about available syntax, refer to the [Pattern syntax reference for JVM](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html).

### Define the text you plan to search in

1. Introduce a local variable `text` with the keyword `val`. 
2. Assign the following value to the `text` variable: Actomyosin, 99, actor, 123, actress, 808, actual, 5005, actually, actuary.

   ```kotlin
   val text = "Actomyosin, 99, actor, 123, actress, 808, actual, 5005, actually, actuary"
   ```

> In this tutorial, we will use a list of words and numbers as mock data. You can also use the text of your choice. In this case, you will need to configure a search pattern that will be relevant for your text, but you still can refer to the described functions.
>

### Define the pattern to search with

1. Introduce a local variable `pattern` with the keyword `val`. 
2. Assign the `\b[1-9][0-9]{2}\b` value to this variable.

   ```kotlin
   val pattern = "\b[1-9][0-9]{2}\b"
   ```

With this regular expression, you can search for numbers between 100 and 999.

3. Add an extra backslash before each `\b` part of the regular expression. 

   `\b` is a metacharacter with a special meaning. This metacharacter matches a number boundary. You must use `\` as an escape character before metacharacters. Otherwise, the compiler will ignore the special meaning of metacharacters. 

   ```kotlin
   val pattern = "\\b[1-9][0-9]{2}\\b"
   ```

3. For now, your pattern is just a text string. To make it into a regular expression, assign the `Regex` type to the value.

   ```kotlin
   val pattern = Regex("\\b[1-9][0-9]{2}\\b")
   ```

In this example, we added the `Regex` type to the value. Alternatively, you can use the `toRegex` function.

   ```kotlin
   val pattern = "\\b[1-9][0-9]{2}\\b".toRegex()
   ```

> In this tutorial, we will search for numbers between 100 and 999. You can also create a search pattern of your choice. In this case, you will need to have a relevant text for your pattern, but you still can refer to the described functions.
>

## Search with a pattern

In this part, you will learn how to:

* Find out if the text contains any matches of your pattern ([`containsMatchIn`](#containsMatchIn--finds-out-if-the-text-contains-any-matches))
* Find the first pattern match in the text ([`find`](#find--finds-the-first-match))
* Find all pattern matches in the text ([`findAll`](#findAll--finds-all-matches))
* Find out if your pattern matches the whole text; depending on the applied function, you can get a match parameter ([`matchEntire`](#matchentire--finds-out-if-the-pattern-matches-the-whole-text-returns-a-match-parameter)) or a Boolean value ([`matches`](#matches--finds-out-if-the-pattern-matches-the-whole-text-returns-a-boolean-value)).

You can find the full list of functions provided by the `Regex` type in the [reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/#kotlin.text.Regex).

### containsMatchIn — finds out if the text contains any matches 

The `containsMatchIn` function attempts to can find a match of the regular expression in your text.

Define if the pattern has a match in the text.

1. Define your [text](#define-the-text-you-plan-to-search-in) and [search pattern](#define-the-pattern-to-search-with) as local variables.

   ```
   val text = "Actomyosin, 99, actor, 123, actress, 808, actual, 5005, actually, actuary"
   val pattern = Regex("\\b[1-9][0-9]{2}\\b")
   ```

3. Introduce a local variable `result1` with the keyword `val`.

   ```
   val result1 
   ```

4. Assign the following value to the `result1` variable:

   ```
   pattern.containsMatchIn(text)
   ```

   where:
   * `pattern` is a variable for the search pattern
   * `containsMatchIn` is a search function
   * `text` is a variable for the text where we are searching for matches

5. Use the `println` function to display the result of the `result1` variable.

   ```kotlin
   fun main() {

      val text = "Actomyosin, 99, actor, 123, actress, 808, actual, 5005, actually, actuary"
      val pattern = Regex("\\b[1-9][0-9]{2}\\b")
      val result1 = pattern.containsMatchIn(text)
   
      println("The containsMatchIn function returns $result1.") //true

   }
   ```
   
6. To run your application, click the green **Run** icon in the gutter and select **Run 'MainKt'**.

The pattern has matches in the text, so the `containsMatchIn` function returns the `true` value.

### find — finds the first match

The `find` function returns the first match of a regular expression in the text. 

Find the first match of the pattern in the text.

1. Define your [text](#define-the-text-you-plan-to-search-in) and [search pattern](#define-the-pattern-to-search-with) as local variables.

   ```
   val text = "Actomyosin, 99, actor, 123, actress, 808, actual, 5005, actually, actuary"
   val pattern = Regex("\\b[1-9][0-9]{2}\\b")
   ```

2. Introduce a local variable `result2` with the keyword `val`. 

   ```
   val result2
   ```

3. Assign the following value to the `result2` variable: 
 
   ```
   pattern.find(text)
   ```

   where:
   * `pattern` is a variable for the search pattern
   * `find` is a search function
   * `text` is a variable for the text where we are searching for matches
   
4. Use the `println` function to display the result of the `result2` variable and the `value` function to get the first number that matches the regular expression. 

   If the pattern does not have matches in the text, the `find` function returns `null`. To allow the `value` function to return `null`, add a question mark `?` after the          `result2` variable name. For information about the danger of null references, refer to [Null Safety](https://kotlinlang.org/docs/reference/null-safety.html).

   ```kotlin
   fun main() {

      val text = "Actomyosin, 99, actor, 123, actress, 808, actual, 5005, actually, actuary"
      val pattern = Regex("\\b[1-9][0-9]{2}\\b")
      val result2 = pattern.find(text)
   
      println("The find function returns ${result2?.value}.") //123
   
   }
   ```
   
5. To run your application, click the green **Run** icon in the gutter and select **Run 'MainKt'**.

The function returns the first match in the list: `123`.

For information about function parameters and exceptions, refer to the [`find` function reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/find.html). 

### findAll — finds all matches

The `findAll` returns all matches of the regular expression in your text. 

Find all pattern matches in the text.

1. Define your [text](#define-the-text-you-plan-to-search-in) and [search pattern](#define-the-pattern-to-search-with) as local variables.

   ```
   val text = "Actomyosin, 99, actor, 123, actress, 808, actual, 5005, actually, actuary"
   val pattern = Regex("\\b[1-9][0-9]{2}\\b")
   ```

2. Introduce a local variable `result3` with the keyword `val`.

   ```
   val result 3
   ```

3. Assign the following value to the `result3` variable:

   ```
   pattern.findAll(text)
   ```

   where:
   * `pattern` is a variable for the search pattern
   * `findAll` is a search function
   * `text` is a variable for the text where we are searching for matches

4. Use the `println` function to display the text presenting results of the `result3` variable.

   ```
    println("The findAll function returns")
   ```
   
5. The result of the `findAll` function is a sequence of values. Use the `value` function to get the list of numbers that match the regular expression and the `forEach` function to display the result as a column of values. For information about this function, refer to the [`forEach` function reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/for-each.html).

   ```kotlin
   fun main() {

       val text = "Actomyosin, 99, actor, 123, actress, 808, actual, 5005, actually, actuary"
       val pattern = Regex("\\b[1-9][0-9]{2}\\b")
       val result3 = pattern.findAll(text)
       
       println("The findAll function returns")
       result3.forEach { match ->
         val values = match.value
         println(values) //123, 808
      }
   
   }
   ```

6. To run your application, click the green **Run** icon in the gutter and select **Run 'MainKt'**.

The pattern has two matches in the text: `123` and `808`, so the `findAll` function returns 2 values.

For information about function parameters and exceptions, refer to the [`findAll` function reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/find-all.html).

### matchEntire — finds out if the pattern matches the whole text; returns a match parameter

The `matchEntire` function attempts to match the regular expression against the entire text string. 

Define if the pattern matches the entire text.

1. Define your [text](#define-the-text-you-plan-to-search-in) and [search pattern](#define-the-pattern-to-search-with) as local variables.

   ```
   val text = "Actomyosin, 99, actor, 123, actress, 808, actual, 5005, actually, actuary"
   val pattern = Regex("\\b[1-9][0-9]{2}\\b")
   ```

2. Introduce a local variable `result4` with the keyword `val`. 

   ```
   val resul4
   ```

3. Assign the following value to the `result4` variable:

   ```
   pattern.matchEntire(text)
   ```

   where:
   * `pattern` is a variable for the search pattern
   * `matchEntire` is a search function
   * `text` is a variable for the text where we are searching for matches

4. Use the `println` function to display the result of the `result4` variable. Use the `value` function to get a range of indexes in the text string. 

   If the pattern does not have matches in the text, the `matchEntire` function returns `null`. To allow the `range` function to return `null`, add the question mark `?` after    the `result4` variable name. For information about the danger of null references, refer to [Null Safety](https://kotlinlang.org/docs/reference/null-safety.html).

   ```kotlin
   fun main() {

      val text = "Actomyosin, 99, actor, 123, actress, 808, actual, 5005, actually, actuary"
      val pattern = Regex("\\b[1-9][0-9]{2}\\b")
      val result4 = pattern.matchEntire(text)
   
      println("The matchEntire function returns ${result4?.range}") //null
      
   }
   ```

5. To run your application, click the green **Run** icon in the gutter and select **Run 'MainKt'**.

The pattern does not match the text, so the function returns `null`.

### matches — finds out if the pattern matches the whole text; returns a Boolean value

The `matches` function indicates whether the regular expression matches the entire text string. 

Define if the pattern matches the entire text.

1. Define your [text](#define-the-text-you-plan-to-search-in) and [search pattern](#define-the-pattern-to-search-with) as local variables.

   ```
   val text = "Actomyosin, 99, actor, 123, actress, 808, actual, 5005, actually, actuary"
   val pattern = Regex("\\b[1-9][0-9]{2}\\b")
   ```

2. Introduce a local variable `result5` with the keyword `val`.

   ```
   val result5
   ```

3. Assign the following value to the `result5` variable:

   ```
   pattern.matches(text)
   ```

   where:
   * `pattern` is a variable for the search pattern
   * `matches` is a search function
   * `text` is a variable for the text where we are searching for matches

4. Use the `println` function to display the result of the `result5` variable.

   ```kotlin
   fun main() {

   val text = "Actomyosin, 99, actor, 123, actress, 808, actual, 5005, actually, actuary"
   val pattern = Regex("\\b[1-9][0-9]{2}\\b")
   val result5 = pattern.matches(text)
    
   println("The matches function returns $result5") //false
   
   }
   ```
    
5. To run your application, click the green **Run** icon in the gutter and select **Run 'MainKt'**.

The pattern does not match the text, so the function returns the `false` value.

## What's next?

In this tutorial, we explained how to write patterns with regular expressions and use these patterns for searching data in a text. To extend this knowledge, you can:
* Add options to your regular expression using the [`RegexOption` type reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex-option/)
* Replace data in the text using [other functions of the `Regex` type](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/#kotlin.text.Regex$replace(kotlin.CharSequence,%20kotlin.String)/input)
