---
title: Flutter basics
date: 2021-12-12
author: m0wer
tags: [ 'basics' ]
---

# Usage

## Commands

* `flutter --version`: See Flutter and Dart version.

# Operators

## .?

Use `?.` when you want to call a method/getter on an object if that object is
not null (otherwise, return null).

Example:

```dart
currentState?.open();
```

## ?? (if null)

Get a default value if object is null:

```dart
var value;
...
value = value ?? 2;
```

# Built-in data types

## Enum

```dart
enum Day { monday, tuesday }
```

### Get the value of an enum element

```dart
Day.monday.name
```

## List

### Find first element that satisfies condition

Use `.firstWhere()`:

```dart
List<Currency> currencies = ...;
Currency dollar = currencies.firstWhere((currency) => currency.code == "USD");
```

## Map

```dart
Map<String, int> myMap = {
    "apple": 3,
    "orange": 5,
  };
```

### Iterate through map entries (keys and values)

```dart
List<String> myList = myMap.entries.map(
                                        (var entry) =>
                                        "${entry.key}: ${entry.value}"
                                       ).toList();
```

### Combine/merge/concat maps

You can use spread operator `...`:


```dart
final firstMap = {"1":"2"};
final secondMap = {"2":"3"};

final thirdMap = {
   ...firstMap,
   ...secondMap,
};
```

# Writing documentation

Add comments with `//` or `///`, the later will make the comments be
included by [`dartdoc`](https://github.com/dart-lang/dartdoc).

Rules:

* DO format comments like sentences (capitalization and punctuation).
* DON’T use block comments for documentation.
* DO use `///` doc comments to document members and types in the preceding
  line.
* DO start doc comments with a single-sentence summary and continue after
  an empty comment line if necessary.

## Generate the docs

Run

```bash
flutter pub global run dartdoc:dartdoc
```
