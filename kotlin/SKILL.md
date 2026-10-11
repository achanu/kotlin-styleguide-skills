---
name: kotlin
description: The official Android Kotlin style guide. Covers source file structure, brace style, whitespace, 4-space indentation, 100-char column limit, naming conventions (PascalCase classes, camelCase functions, UPPER_SNAKE_CASE constants), and KDoc documentation. Enforces idiomatic Kotlin with no semicolons, no wildcard imports, and explicit types in public APIs.
---

# Android Kotlin Style Guide

> Google's Android coding standards for Kotlin source code.

## Golden Rules

1. **UTF-8, 4-space indentation** — never tabs
2. **No semicolons** — one statement per line
3. **No wildcard imports** — single ASCII-sorted list
4. **K&R braces** — opening brace on the same line, break before `else`
5. **100-character column limit** — wrap at higher syntactic level
6. **PascalCase types, camelCase functions, UPPER_SNAKE_CASE constants**
7. **KDoc on public types and members** — starts with a summary fragment

## Quick Reference

### Naming Conventions

| Element | Convention | Example |
|---|---|---|
| Packages | all lowercase, no underscores | `com.example.deepspace` |
| Classes/Interfaces | PascalCase nouns or adjectives | `ImmutableList`, `Readable` |
| Test classes | name + `Test` suffix | `HashTest` |
| Functions | camelCase verbs | `sendMessage` |
| `@Composable` Unit functions | PascalCase nouns | `NameTag()` |
| Constants | UPPER_SNAKE_CASE | `EMPTY_ARRAY` |
| Properties/locals/params | camelCase | `defaultExtension` |
| Backing properties | `_` prefix, same name | `_table` |
| Type variables | single capital or `...T` | `T`, `RequestT` |
| Test functions | underscores allowed | `pop_emptyStack` |

### Braces and Expressions

```kotlin
// ✓ CORRECT - K&R style, no break before else
if (list.isEmpty()) {
    return
} else {
    process(list)
}

// ✗ INCORRECT - no space before brace, no break before else
if (list.isEmpty()){
    return
}else{
}
```

### Whitespace

```kotlin
// ✓ CORRECT
class Foo : Runnable
val two = 1 + 1
ints.map { value -> value.toString() }

// ✗ INCORRECT
class Foo: Runnable
val two = 1+1
ints.map { value->value.toString() }
```

### Constants

```kotlin
// ✓ CORRECT - deeply immutable, const for scalars
const val NUMBER = 5
val NAMES = listOf("Alice", "Bob")

// ✗ INCORRECT - mutable state is not a constant
val AGES = mapOf("Alice" to mutableInstance)
```

### KDoc

```kotlin
// ✓ CORRECT - brief summary fragment first, blank line before tags
/**
 * Formats the given date.
 *
 * @param date the date to format
 * @return the formatted date
 */
fun formatDate(date: Date): String { }

// ✗ INCORRECT - complete sentence starting with "This method"
/** This method formats the date. */
```

## Common Mistakes

| Mistake | Correct Approach |
|---|---|
| Semicolons at end of statements | Omit semicolons entirely |
| `class Foo: Runnable` | Space before colon in supertype: `class Foo : Runnable` |
| Wildcard imports (`import java.util.*`) | Import each name explicitly |
| Hungarian notation (`mName`, `s_name`, `kName`) | Plain camelCase; `_` only for backing properties |
| `XMLHTTPRequest` style acronyms | `XmlHttpRequest` — lowercase everything, then capitalize |
| Missing KDoc on public types | KDoc for every public type/member |
| Backtick function names with spaces | `fun testEveryPossibleCase()` |
| Tabs for indentation | 4 spaces per block level |
| Explicit types on private inferred values | Omit unless part of public API |

## Install

```bash
npx skills add achanu/kotlin-styleguide-skills/kotlin
```

## Full Guide

See [kotlin.md](kotlin.md) for complete details, examples, and edge cases.
