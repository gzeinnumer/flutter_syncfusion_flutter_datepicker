# flutter_syncfusion_flutter_datepicker

|<img src="/preview/preview1.png" width="300"/>|
|--|

```dart
import 'package:flutter/material.dart';

import 'package:intl/intl.dart';
import 'package:syncfusion_flutter_datepicker/datepicker.dart';

void main() {
  return runApp(MyApp());
}

//https://pub.dev/packages/syncfusion_flutter_datepicker
class MyApp extends StatefulWidget {
  @override
  MyAppState createState() => MyAppState();
}

class MyAppState extends State<MyApp> {
  String _selectedDate = '';
  String _dateCount = '';
  String _range = '';
  String _rangeCount = '';

  void _onSelectionChanged(DateRangePickerSelectionChangedArgs args) {
    setState(() {
      if (args.value is PickerDateRange) {
        _range = '${DateFormat('dd/MM/yyyy').format(args.value.startDate)} -'
            // ignore: lines_longer_than_80_chars
            ' ${DateFormat('dd/MM/yyyy').format(args.value.endDate ?? args.value.startDate)}';
        print("zein_1_${_range}");
      } else if (args.value is DateTime) {
        _selectedDate = args.value.toString();
        print("zein_2_${DateFormat('yyyy-MM-dd').format(args.value)}");
      } else if (args.value is List<DateTime>) {
        _dateCount = args.value.length.toString();
        for (var i = 0; i < args.value.length; i++) {
          print("zein_3_${DateFormat('yyyy-MM-dd').format(args.value[i])}");
        }
      } else {
        _rangeCount = args.value.length.toString();
        print("zein_3_${_rangeCount}");
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: const Text('DatePicker demo'),
        ),
        body: Stack(
          children: <Widget>[
            Positioned(
              left: 0,
              right: 0,
              top: 0,
              height: 80,
              child: Column(
                mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                mainAxisSize: MainAxisSize.min,
                crossAxisAlignment: CrossAxisAlignment.start,
                children: <Widget>[
                  Text('Selected date: $_selectedDate'),
                  Text('Selected date count: $_dateCount'),
                  Text('Selected range: $_range'),
                  Text('Selected ranges count: $_rangeCount'),
                ],
              ),
            ),
            Positioned(
              left: 0,
              top: 80,
              right: 0,
              bottom: 0,
              child: SfDateRangePicker(
                onSelectionChanged: _onSelectionChanged,
                // selectionMode: DateRangePickerSelectionMode.range,
                // selectionMode: DateRangePickerSelectionMode.extendableRange,
                selectionMode: DateRangePickerSelectionMode.multiple,
                // selectionMode: DateRangePickerSelectionMode.single,
                initialSelectedRange: PickerDateRange(
                  DateTime.now().subtract(const Duration(days: 4)),
                  DateTime.now().add(
                    const Duration(days: 3),
                  ),
                ),
              ),
            )
          ],
        ),
      ),
    );
  }
}
```

---

```
Copyright 2023 M. Fadli Zein
```