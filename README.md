# Flutter Local Notifications Provider

[![pub package](https://img.shields.io/pub/v/flutter_local_notifications_provider.svg)](https://pub.dartlang.org/packages/flutter_local_notifications_provider)


It adds a functionality in the [main package ](https://github.com/MaikuB/flutter_local_notifications/).

## Features

* Adding FlutterLocalNotificationsPlugin into Widget Tree via InheritedWidget

## Example

After you are done with basic setup, you just need to add this into Widget Tree

```dart
@override
Widget build(BuildContext context) {
    return NotificationProvider(
        service: flutterLocalNotificationsPlugin,
        child: MaterialApp(
            title: 'Title',
            theme: new ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: widget.home),
    );
}
```

`NotificationProvider` needs plugins's reference.

You can access it using `NotificationProvider.of(context);`, for example:

```dart
...
        child: RaisedButton(
          onPressed: () async {
            await _showNotification(context);
          },
          child: Text('Test with notification'),
        ),
....

  Future _showNotification(BuildContext context) async {
    var plugin = NotificationProvider.of(context);
    var androidPlatformChannelSpecifics = AndroidNotificationDetails(
        'your channel id', 'your channel name', 'your channel description',
        importance: Importance.Max, priority: Priority.High);
    var iOSPlatformChannelSpecifics = IOSNotificationDetails();
    var platformChannelSpecifics = NotificationDetails(
        androidPlatformChannelSpecifics, iOSPlatformChannelSpecifics);
    await plugin.show(0, 'Title', 'Description',
        platformChannelSpecifics);
  }
```