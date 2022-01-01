---
title: Flutter Provider
date: 2022-01-01
author: m0wer
---

A relatively simple and efficient tool for state management in Flutter is
[provider](https://pub.dev/packages/provider).


# Usage

## ChangeNotifierProxyProvider

When an provider needs information from another, use
`ChangeNotifierProxyProvider`.


```dart
class MyModel with ChangeNotifier {
  ...
  }

}
class MyChangeNotifier with ChangeNotifier {
  void update(MyModel myModel) {
    // Do some custom work based on myModel that may call `notifyListeners`
  }
}

ChangeNotifierProxyProvider<MyModel, MyChangeNotifier>(
  create: (_) => MyChangeNotifier(),
  update: (_, myModel, myNotifier) => myNotifier
    ..update(myModel),
  child: ...
);
```

Pass the provider dependency as the first argument, which must be declared
already (e.g., as a `ChangeNotifierProvider` in a `MultiProvider`).
