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
