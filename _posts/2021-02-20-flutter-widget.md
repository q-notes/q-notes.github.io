---
layout: post
title:  "Flutter Widget"
date:   2021-02-20 10:25:00 +0700
tags:   flutter
---

## Hello world

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(
    Center(
      child: Text(
        'Hello, world!',
        textDirection: TextDirection.ltr,
      ),
    ),
  );
}
```

The `runApp()` function takes the given Widget and makes it the root of the widget tree. In this example, the widget tree consists of two widgets, the `Center` widget and its child, the `Text` widget.

When writing an app, you’ll commonly author new widgets that are subclasses of either `StatelessWidget` or `StatefulWidget`, depending on whether your widget manages any state.

## Stateless Widget
A widget’s main job is to implement a `build()` function, which describes the widget in terms of other, lower-level widgets.

Stateless widgets are immutable, meaning that their properties can’t change—all values are final.

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Welcome to Flutter',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Welcome to Flutter'),
        ),
        body: Center(
          child: Text('Hello World'),
        ),
      ),
    );
  }
}
```

This example creates a Material app. The `Scaffold` widget, from the Material library, provides a default app bar, and a body property that holds the widget tree for the home screen.

## Stateful Widget
Stateful widgets maintain state that might change during the lifetime of the widget.

Implementing a stateful widget requires at least two classes: 1) a `StatefulWidget` class that creates an instance of 2) a `State` class.

The `StatefulWidget` class is, itself, immutable and can be thrown away and regenerated, but the `State` class persists over the lifetime of the widget.

```dart
class Counter extends StatefulWidget {
  @override
  _CounterState createState() => _CounterState();
}

class _CounterState extends State<Counter> {
  int _counter = 0;

  void _increment() {
    setState(() {
      // This call to setState tells the Flutter framework that
      // something has changed in this State, which causes it to rerun
      // the build method below so that the display can reflect the
      // updated values. If you change _counter without calling
      // setState(), then the build method won't be called again,
      // and so nothing would appear to happen.
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    // This method is rerun every time setState is called,
    // for instance, as done by the _increment method above.
    return Row(
      children: <Widget>[
        ElevatedButton(
          onPressed: _increment,
          child: Text('Increment'),
        ),
        Text('Count: $_counter'),
      ],
    );
  }
}
```
