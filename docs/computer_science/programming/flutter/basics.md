---
title: Flutter basics
date: 2021-12-12
author: m0wer
tags: [ 'basics' ]
---

# Built-in data types

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
