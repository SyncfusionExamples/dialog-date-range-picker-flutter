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
