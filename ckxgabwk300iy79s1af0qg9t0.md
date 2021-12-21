## Vitess LFX Mentorship Fall 2021

I recently graduated from LFX Mentorship Program. In this blog post, I will be sharing my experience of contributing to [Vitess](https://vitess.io/), a database clustering system for horizontal scaling of MySQL.

## What is LFX Mentorship

In the exact words of the Linux Foundation, 

>The Linux Foundation Mentorship Program is designed to help developers — many of whom are first-time open source contributors — with the necessary skills and resources to learn, experiment, and contribute effectively to open source communities. By participating in a mentorship program, mentees have the opportunity to learn from experienced open source contributors as a segue to get internship and job opportunities upon graduation."

This sounded quite fascinating to me and aligned with my goals. That's how I get all excited for this program.

## Why Vitess?

During this term, I had to study Database Management Systems as a part of my college curriculum, and I had previous experience with MySQL, so I applied to the project [CNCF - Vitess: Add support for comparing strings using collations and character-sets](https://mentorship.lfx.linuxfoundation.org/project/058a41fd-79e8-43f7-a5f7-1840c1f759be)

Also, I was particularly fascinated by the extent of usage of Vitess. It was built by intelligent people at Youtube to manage their database load and used by Github, Slack, Pinterest, etc.

## Problem Statement of Project

Vitess does not yet have support for collations and character sets. So, to compare varchar strings, Vitess needs to rely on [WEIGHT_STRING](https://dev.mysql.com/doc/refman/5.7/en/string-functions.html#function_weight-string) function for now. MySQL documentation says WEIGHT_STRING is a debugging function meant only for internal use. 

![my reaction](https://media.giphy.com/media/l0Iy1U0KU3rBaewjm/giphy-downsized.gif)

### Use Cases

- Having the ability to compare strings using collation and character-set support, it would be possible to better implement ORDER BY, GROUP BY, JOIN.
- It would be possible to leverage more advanced join techniques than currently implemented.

## Plan Out

The initial plan that can be found in the project issue was to use `text/collate` package. We decided to make its fork and make it suitable for our use case.

We tried our hands to replicate MySQL's `WEIGHT_STRING` using the package but had no success because:
> It only supports UCA compatible collations while MySQL supports several non-UCA collations as well. So in turn Vitess needs to support them too.

So we headed onto the MySQL [codebase](https://github.com/king-11/mysql-server/tree/vitess)

![onto MySQL](https://media.giphy.com/media/PkS3n3TERbjIntnx9E/giphy.gif)

## Dive into MySQL

### Unit Testing Before Anything

The collations implementation in MySQL is part of the MySQL codebase. The first task that my mentor assigned to me was transpiling tests from MySQL to Vitess. It felt weird to me because who writes code first, right?... Guess what I later realized it is a well-known approach called **Test-Driven Development**.

![unit testing](https://media.giphy.com/media/MgBJ3UifivIY/giphy.gif)

MySQL had two types of tests, ones that are normal Unit Tests others that are Benchmarking tests. I transpiled both as Unit Tests into Vitess for starters.

### Collation Transpilation

MySQL has a lot of different charsets; only a few of them are based on the Unicode Collation Algorithm (UCA). UCA collations are implemented in [golang/text](https://pkg.go.dev/golang.org/x/text). Other collations are custom and need to be ported directly from MySQL.

### Extra Collations

[conf_to_src](https://github.com/mysql/mysql-server/blob/8.0/strings/conf_to_src.cc) is responsible for generating charset data for `extra` charsets in MySQL. So I was supposed to port this to Vitess.

For parsing the XML Data maps, I learned to use [encoding/xml](https://pkg.go.dev/encoding/xml) as I was pretty new to golang and its patterns. [Vicent Marti](https://twitter.com/vmg), my mentor, helped me a lot by providing me reviews and making me understand go patterns and how to write better, more robust code.

Parsing the XML Charsets was a recursive process where you needed to drop down to levels and merge with previously found charsets their collations.

### UCA Tailorings

UCA collations are built on the `utf8_0900` collation, where they modify the standard weight as per language needs. Those modifications are called [tailorings](https://unicode.org/reports/tr10/#Tailoring). Each UCA collation specifies tailorings which then are responsible for modifying weights.

Example: `a <<< A << à <<< À < b <<< B`

I was to understand the UCA tailoring syntax, copy over the tailorings from MySQL and make a parser to make modifications.

Vicent had a new idea that instead of parsing those strings, we can use the parsing done by MySQL by utilizing the in-memory weights. For that, we decided to dump the UCA weights in JSON using a custom test for each collation.

After that, we diff the ones different from the original UCA weights into separate Go source code that makes our tailorings.

### License Issues

Due to Vitess and Oracle license issues, we can't parse the XML as we were doing using `conf_to_src`. The license only allows us to use in-memory things. So we dump those collations as JSON by attaching to MySQL Unit Testing with a custom unit test and then convert them into `go` code. 

![license issue](https://media.giphy.com/media/3o6Mb5N2oCnG4dMvIc/giphy.gif)

So instead of using `encoding/xml`, I switched to `encoding/json`, and we were good to go with a few structural changes. At certain places, I was using `regex`, which vicent amended to use `bufio` robust architecture instead.

**Result:**

%[https://github.com/vitessio/vitess/pull/8991]

## Collation Module Integration

After the `mysql/collations` module was in Vitess we had a meeting with Andres, Harshit, Florent, Vicent and me. In that meeting, we decided on the next step which was integrating the module into Vitess's Evaluation Engine.

Function `NullSafeCompare` is the one that is used for any form of comparison in Vitess. For `Text` comparisons is used to return an unsupported type error.

To make it collation aware I added another parameter into its definition that is the `collationID`. If the `ID` isn't `0` and we get a collation from `collations` module lookup function then we use it to collate the values.

Similar to `NullSafeCompare` we had `Min`, `Max` and `minmax` which were made collation aware so that they can use `NullSafeCompare` as it needs to be. Unit tests were added similar to ones in MySQL to test the new capabilities of these functions.

So, all the places that were using `NullSafeCompare` now were supposed to pass down collation information but for starters I just made them pass a `0` and added in TODO.

```go
v1, v2 := "c", "cs"
// hungarian accent insensitive case insensitive collation
max, _ := Max(v1, v2, "utf8mb4_hu_0900_ai_ci")
// max == "cs"
```

## Aggregates and GroupBy

The `OrderedAggregate` struct was missing collation information it only contained the default charset information in it. To add collation information into semantic analysis Andres and Florent started working on [gen4: add collation name to the type definition](https://github.com/vitessio/vitess/pull/9038).

Through PR #4038 Collations were made available throughout the planning phase using semTable's `CollationFor(expr sqlparser.Expr)` method. Using this method, `OrderedAggregate` was now aware of its grouping keys' collations.

OA has two methods which call in `NullSafeCompare` those are:
- keysEqual
- merge

Collations are fetched from OA as a `map[int]collations.ID` because not all columns have collation info so helps to reduce space requirements.

The map is then passed down to the above functions. If rows with respect to GroupByKeys are equal then they are merged. Aggregation is done based on the opCode for that particular aggregation which in turn might call the new `Min` and `Max`.

Finally, unit testing was done for grouping using various collations like case insensitive, accent sensitive and kana sensitive ones.

The following example when grouped using a case and accent insensitive collation:

| col | count |
|:---:|:---:|
| a | 1 |
| A | 1 |
| Ǎ | 1 |
| ß | 11 |
| ss | 2 |

results in:

| col | count |
|:---:|:---:|
| a | 3 |
| ß | 13 |

**Result:**

%[https://github.com/vitessio/vitess/pull/9018]

## Memory, Route and Merge Sort

### Comparer

All these methods are connected by a single struct i.e. `engine.comparer`. The struct contains details about which column to use for ordering and whether it needs to be descending or not.

It made sense to include collation information too in the struct for ease of access wherever required. Now when calling `comparer.compare` we can access collation ID and pass it down to the `NullSafeCompare` call inside the function body.

A new `comparer` is made from the `OrderByParams` so they need to carry the collation information as well in form of a new field.

### Order By Params

`OrderByParams` are created using the `planbuilder` module. To get collation ID we use the `semTable.CollationFor(expr sqlparser.Expr)`.

- For planning Route Sort it already contains details about order `abstract.OrderBy`. Order contains the expression for the statement on which we can call `CollationFor` providing us with Collation ID.
- Creating a memory sort plan on aggregation we first need to find the expression that matches our order expression. If we get a match with one of our GroupByKeys then we can access its collation ID for use.
- For memory sort planning with `planningContext` is similar to route sort we just have to access the semantic table using the context.

### Unit Testing

Based on the already present tests for weight string sort with Memory and Route sort testing was done for:
- Ordering by Hungarian Collation
- Descending Order Sorting
- Upper Limit for returned entries
- Error with Unknown Collation
- Error with Unsupported Collation

### E2E Testing

Unit testing only tested memory, merge and route sort separately. To test Memory Sort on aggregation we needed to look at E2E tests.

To add collation details to the Order By statement we updated the `String()` method to add in the `COLLATE` statement as well with it.

We then updated the aggregation cases to carry collate information in the OrderBy field to be properly able to test the feature. For this, I had to pair code with Andres and Florent because I wasn't much familiar with eval engine testing.

**Result:**

%[https://github.com/vitessio/vitess/pull/9155]

## Learnings

A three-month-long journey and I got to learn so many things:

![skilling up](https://media.giphy.com/media/5RpWGcd0D8siGo5oCB/giphy.gif)

- Got familiar with golang that too in a project which was one of the early adopters of go.
- I better understand why the design patterns are used in language and can also better implement them.
- Went into a deep dive about string representation in charsets and Unicode which was a prerequisite of the project. [Interesting Read](https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/)
- Got to take a look at the inner workings of MySQL and its humongous codebase and test suite.
- I became collation aware just like Vitess :)

## End on High Note

I am very thankful to [Vicent](https://twitter.com/vmg) for walking me through the mentorship. The reviews I received from him and pair coding under his supervision really helped me grow as a programmer.

Also wanna thank [Florent](https://www.linkedin.com/in/florent-poinsard) and [Andres](https://www.linkedin.com/in/andrestaylor) who were working alongside me on this project and really helped me wherever was needed.

Lastly, I did like to thank my mentor [Shivansh Saini](https://www.linkedin.com/in/shivanshs9/) for always being a motivation, always will be and one of the reasons I applied for LFX.

![thanks](https://media.giphy.com/media/lD76yTC5zxZPG/giphy.gif)
