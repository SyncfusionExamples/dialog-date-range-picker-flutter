# How to add a date range picker (SfDateRangePicker) in the Flutter dialog window

In an application, the date range picker can be displayed in a dialog window by using the `onPressed` event of the button.

## Step 1:
To host a date range picker in a pop-up, you can use the 'AlertDialog' window to achieve this add the date range picker inside the alert dialog and open the dialog on the 'onpressed' event of a button. Here, a flat button is used.

```xml
body: Column(
  mainAxisAlignment: MainAxisAlignment.center,
  crossAxisAlignment: CrossAxisAlignment.stretch,
  children: <Widget>[
    FlatButton(
      child: Container(
        child: _selectedDate ==null
            ? Text('Select a date'):Text(_selectedDate),
      ),
      onPressed: () {
        showDialog(
            context: context,
            builder: (BuildContext context) {
              return AlertDialog(
                  title: Text(''),
                  content: Container(
                    height: 350,
                    child: Column(
                      children: <Widget>[
                        getDateRangePicker(),
                        FlatButton(
                          child: Text("OK"),
                          onPressed: () {
                            Navigator.pop(context);
                          },
                        )
                      ],
                    ),
                  ));
            });
      },
    ),
  ],
));
 
Widget getDateRangePicker() {
  return Container(
      height: 250,
      child: Card(
          child: SfDateRangePicker(
        view: DateRangePickerView.month,
        selectionMode: DateRangePickerSelectionMode.single,
        onSelectionChanged: selectionChanged,
      )));
}
```
 

## Step 2:
Using the `onSelectionChanged` event, you can show the selected date of the picker.

```xml
void selectionChanged(DateRangePickerSelectionChangedArgs args) {
  _selectedDate = DateFormat('dd MMMM, yyyy').format(args.value);
 
  SchedulerBinding.instance.addPostFrameCallback((duration) {
    setState(() {});
  });
}
```
**[View document in Syncfusion Flutter Knowledge base](https://www.syncfusion.com/kb/11467/how-to-add-a-date-range-picker-sfdaterangepicker-in-the-flutter-dialog-window)**

**Screenshots**

<img alt="selected date text"  src="http://www.syncfusion.com/uploads/user/kb/flut/flut-891/flut-891_img1.png" width="250" height="250" />|
<img alt="picker with selected date"  src="http://www.syncfusion.com/uploads/user/kb/flut/flut-891/flut-891_img2.png" width="200" height="250" />|
<img alt="date details"  src="http://www.syncfusion.com/uploads/user/kb/flut/flut-891/flut-891_img3.png" width="250" height="250" />|
