# Android Kotlin Style Guide

> Source: https://developer.android.com/kotlin/style-guide

This is the complete definition of Google's Android coding standards for Kotlin
source code. A file is in Google Android Style if and only if it adheres to
these rules.

---

## 1. Source Files

All source files must be encoded as UTF-8.

### File naming

- Single top-level class: file name is the case-sensitive class name + `.kt`.
- Multiple top-level declarations: PascalCase name describing the contents
  (camelCase acceptable if plural), + `.kt`.

```kotlin
// MyClass.kt - single top-level class: name matches the class
class MyClass { }

// Map.kt - multiple declarations: descriptive PascalCase name
fun <T, O> Set<T>.map(func: (T) -> O): List<O> = emptyList()
fun <T, O> List<T>.map(func: (T) -> O): List<O> = emptyList()
```

### Special characters

- Only the ASCII horizontal space appears anywhere in the file; all other
  whitespace in literals is escaped.
- Use special escape sequences (`\b`, `\n`, `\r`, `\t`, `\'`, `\"`, `\\`, `\$`)
  rather than Unicode escapes like `\u000a`.
- For other non-ASCII characters, use the actual character (e.g. `∞`) or the
  Unicode escape — whichever is easier to read. Unicode escapes for printable
  characters are discouraged, and strongly discouraged outside literals and
  comments.

```kotlin
val unitAbbrev = "μs"                          // Best
val unitAbbrev = "\u03bcs" // μs                // Poor: printable escape
return "\ufeff" + content                      // Good: non-printable escape
```

### File structure

A `.kt` file comprises, in order, separated by exactly one blank line:

1. Copyright/license header (optional) — multi-line comment only, never KDoc
   or `//` style
2. File-level annotations (`@file:...`)
3. Package statement — never wrapped, no column limit
4. Import statements — one ASCII-sorted list; wildcard imports are **not
   allowed**; never wrapped
5. Top-level declarations

Files should focus on a single theme (e.g. one public type, or extension
functions on multiple receivers of the same operation). Minimize public
declarations per file. Order contents by some logical order a maintainer could
explain — never simply "chronological by date added". Class members follow the
same rules.

---

## 2. Formatting

### Braces

Braces are optional only for `when` branches and `if` expressions with no more
than one `else` branch that fit on a single line. Otherwise braces are required
for `if`, `for`, `when` branches, `do`, and `while` — even for empty bodies.

```kotlin
// CORRECT
if (string.isEmpty()) return

val result = if (string.isEmpty()) DEFAULT_VALUE else string

when (value) {
    0 -> return
    // ...
}

// INCORRECT - single statement without braces
if (string.isEmpty())
    return  // WRONG!

// INCORRECT - unbraced multi-line chain
if (string.isEmpty()) return  // WRONG
else doLotsOfProcessingOn(string, otherParametersHere)
```

Non-empty blocks follow K&R style: no break before the opening brace, break
after it, break before the closing brace, break after it only if it terminates
a statement or the body of a function/constructor/named class (no break before
`else` or a comma).

```kotlin
return Runnable {
    while (condition()) {
        foo()
    }
}
```

Empty blocks must still be in K&R style:

```kotlin
try {
    doSomething()
} catch (e: Exception) {}  // WRONG!

try {
    doSomething()
} catch (e: Exception) {
}  // Okay
```

An `if/else` used as an expression may omit braces only if the entire
expression fits on one line:

```kotlin
val value = if (string.isEmpty()) 0 else 1  // Okay

val value = if (string.isEmpty()) {  // Okay
    0
} else {
    1
}

val value = if (string.isEmpty())  // WRONG
    0
else
    1
```

### Indentation and statements

- Indent increases by **four spaces** per block; never tabs.
- One statement per line; semicolons are not used.

### Line wrapping

Column limit: **100 characters**. Exceptions: lines where the limit is
impossible (e.g. a long URL in KDoc), `package`/`import` statements, and
cut-and-paste shell commands in comments.

Where to break:

- Break at a **higher syntactic level**.
- Break *after* an operator or infix function name.
- Break *before* the dot separator (`.`, `?.`) and the member reference colons
  (`::`).
- A method/constructor name stays attached to its `(`.
- A comma stays attached to the preceding token.
- A lambda arrow (`->`) stays attached to the preceding argument list.

The goal is clear code, not the fewest lines.

### Functions

When a signature does not fit on one line, break each parameter onto its own
line with a single indent (+4); the closing `)` and return type go on their own
line with no additional indent.

```kotlin
fun <T> Iterable<T>.joinToString(
    separator: CharSequence = ", ",
    prefix: CharSequence = "",
    postfix: CharSequence = ""
): String {
    // ...
}
```

Single-expression functions use expression form:

```kotlin
override fun toString(): String = "Hey"
```

### Properties

Break after the equals sign and indent when an initializer does not fit:

```kotlin
private val defaultCharset: Charset? =
    EncodingRegistry.getInstance().getDefaultCharsetForPropertiesFiles(file)
```

`get`/`set` functions go on their own lines with a normal indent (+4),
formatted like functions:

```kotlin
var directory: File? = null
    set(value) {
        // ...
    }
```

Read-only properties may use the short single-line form:

```kotlin
val defaultExtension: String get() = "kt"
```

---

## 3. Whitespace

### Vertical

A single blank line appears:

- Between consecutive members of a class (optional between two consecutive
  properties with no code between them).
- Between statements, as needed for logical subsections.
- Optionally before the first statement of a function and before/after the
  first/last member of a class.

Multiple consecutive blank lines are permitted but never encouraged.

### Horizontal

A single ASCII space appears (only):

- After reserved words before `(`: `if (`, `for (`, `catch (`.
- Between `}` and a following reserved word: `} else {`.
- Before any open curly brace.
- On both sides of binary operators and the lambda arrow — but **not** around
  `::`, `.`, or the range operator `..`.
- Before a colon **only** in supertype declarations and `where` clauses;
  after a comma or colon everywhere.

```kotlin
// CORRECT
for (i in 0..1) { }
val toString = Any::toString
class Foo : Runnable
fun <T : Comparable<T>> max(a: T, b: T) where T : Comparable<T> {}
ints.map { value -> value.toString() }

// INCORRECT
for(i in 0..1) {}          // missing space after `for`
val two = 1+1              // no spaces around +
ints.map { value->value } // no spaces around ->
Any :: toString           // spaces around ::
it . toString()           // spaces around .
1 .. 4                    // spaces around ..
class Foo: Runnable       // no space before supertype colon
listOf(1,2)               // no space after comma
var debugging = false//disabled by default  // no spaces around //
```

---

## 4. Specific Constructs

### Enum classes

An enum with no functions and no doc on constants may fit on one line:

```kotlin
enum class Answer { YES, NO, MAYBE }
```

Constants on separate lines need no blank line between them unless they define
a body:

```kotlin
enum class Answer {
    YES,
    NO,

    MAYBE {
        override fun toString() = """¯\_(ツ)_/¯"""
    }
}
```

### Annotations

- Member/type annotations go on separate lines immediately before the
  construct; annotations without arguments may share a single line.
- One annotation without arguments may share the declaration line.
- `@[...]` syntax only with an explicit use-site target and only to combine
  two or more annotations without arguments.

```kotlin
@Retention(SOURCE)
@Target(FUNCTION, PROPERTY_SETTER, FIELD)
annotation class Global

@Volatile var disposable: Disposable? = null

@field:[JvmStatic Volatile]
var disposable: Disposable? = null
```

### Implicit return/property types

Omit the type when it is a scalar or clearly inferable from the body:

```kotlin
override fun toString() = "Hey"

private val ICON = IconLoader.getIcon("/icons/kotlin.png")
```

When writing a library, retain explicit types that are part of the public API.

---

## 5. Naming

Identifiers use only ASCII letters, digits, and (rarely) underscores. No
special prefixes/suffixes (`name_`, `mName`, `s_name`, `kName`) except backing
properties.

### Package names

All lowercase, words concatenated, no underscores.

```kotlin
package com.example.deepspace       // Okay
package com.example.deepSpace       // WRONG!
package com.example.deep_space      // WRONG!
```

### Type names

PascalCase, nouns or noun phrases (`Character`, `ImmutableList`). Interfaces
may be adjectives (`Readable`). Test classes: tested class name + `Test`
(`HashTest`, `HashIntegrationTest`).

### Function names

camelCase, verbs or verb phrases (`sendMessage`, `stop`).

- Test functions may use underscores to separate logical components:
  `fun pop_emptyStack()`.
- `@Composable` functions returning `Unit` are PascalCased nouns:
  `fun NameTag(name: String)`.
- Function names must not contain spaces (backtick names are not portable on
  Android): use `testEveryPossibleCase()`, not `` fun `test every possible case`() ``.

### Constant names

UPPER_SNAKE_CASE. A constant is a `val` with no custom `get`, deeply immutable
contents, and no detectable side effects — immutable types, immutable
collections of immutable types, scalars and strings marked `const`. If any
observable state can change, it is not a constant.

```kotlin
const val NUMBER = 5
val NAMES = listOf("Alice", "Bob")
val AGES = mapOf("Alice" to 35, "Bob" to 32)
val COMMA_JOINED = NAMES.joinToString(", ")
val EMPTY_ARRAY = arrayOf<SomeMutableType>()  // scalar type is const-required
```

Constants are only defined inside an `object` or at top level; a constant
valued member of a `class` must use a non-constant name. Scalar constants must
use `const`.

### Non-constant names

camelCase for instance properties, local properties, and parameters:
`variable`, `mutableCollection`, `logger`, `nonEmptyArray`. Typically nouns or
noun phrases.

### Backing properties

Name it exactly as the real property plus an underscore:

```kotlin
private var _table: Map<String, Int>? = null

val table: Map<String, Int>
    get() {
        if (_table == null) {
            _table = HashMap()
        }
        return _table ?: throw AssertionError()
    }
```

### Type variable names

Either a single capital letter, optionally followed by a single numeral
(`E`, `T`, `X`, `T2`), or a class-style name ending in `T` (`RequestT`,
`FooBarT`).

### Camel case

Convert prose to identifiers predictably: ASCII-fold and drop apostrophes,
split into words, lowercase everything (acronyms included), then capitalize
word starts. Original casing is almost entirely disregarded.

| Prose form | Correct | Incorrect |
|---|---|---|
| "XML Http Request" | `XmlHttpRequest` | `XMLHTTPRequest` |
| "new customer ID" | `newCustomerId` | `newCustomerID` |
| "inner stopwatch" | `innerStopwatch` | `innerStopWatch` |
| "supports IPv6 on iOS" | `supportsIpv6OnIos` | `supportsIPv6OnIOS` |
| "YouTube importer" | `YouTubeImporter` | `YoutubeImporter`* |

(* Acceptable, but not recommended.)

Ambiguous hyphenation ("nonempty" vs "non-empty") makes both `checkNonempty`
and `checkNonEmpty` correct.

---

## 6. Documentation (KDoc)

### Formatting

```kotlin
/**
 * Multiple lines of KDoc text are written here,
 * wrapped normally...
 */
fun method(arg: String) {
    // ...
}
```

The single-line form may replace it when the whole block (including markers)
fits on one line and there are no block tags: `/** An especially short bit of KDoc. */`

One blank line (only the aligned leading `*`) separates paragraphs and
precedes the block-tag group.

### Block tags

Standard block tags appear in the order `@constructor`, `@receiver`,
`@param`, `@property`, `@return`, `@throws`, `@see`, and never with an empty
description. Continuation lines indent 4 spaces from the `@`.

### Summary fragment

Each KDoc block begins with a brief summary fragment — a noun or verb phrase,
capitalized and punctuated as a complete sentence, but not one: never
"A `Foo` is a..." or "This method returns...".

### Usage

KDoc is required for every `public` type and every `public`/`protected` member,
except:

- **Self-explanatory functions** — trivially obvious `getFoo`/`foo` members
  where documentation would say only "Returns the foo". Do not use this
  exception to omit information a reader actually needs (e.g. a reader may not
  know what a "canonical name" is).
- **Overrides** — not always present on methods overriding a supertype method.
