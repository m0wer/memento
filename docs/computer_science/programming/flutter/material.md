---
title: Flutter material library
date: 2021-12-12
author: m0wer
tags: [ 'material' ]
---

# Classes

## Color

### Parse hexadecimal color string to Color

```dart
/// Construct a color from a hex code string, of the format #RRGGBB.
Color hexToColor(String code) {
  return new Color(int.parse(code.substring(1, 7), radix: 16) + 0xFF000000);
}
```

## InkWell

Make a component clickable (with animations on hover and tap):

```dart
InkWell(
    onTap: () {
      // To do
    },
    child: Card(),
)
```
