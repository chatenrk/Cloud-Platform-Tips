# Excel Tips useful for Cloud Platform



## Adjust rows macro
This is a temporary macro and needs to be cleaned up later
```sh
  Columns("A:A").Select
    Selection.TextToColumns Destination:=Range("A1"), DataType:=xlDelimited, _
        TextQualifier:=xlDoubleQuote, ConsecutiveDelimiter:=False, Tab:=False, _
        Semicolon:=True, Comma:=False, Space:=False, Other:=False, FieldInfo _
        :=Array(Array(1, 1), Array(2, 1), Array(3, 1), Array(4, 1), Array(5, 1), Array(6, 1), _
        Array(7, 1), Array(8, 1)), TrailingMinusNumbers:=True
    Selection.AutoFilter
    Cells.Select
    Selection.AutoFilter
    Selection.AutoFilter
    ActiveSheet.Range("$A$1:$H$99999").AutoFilter Field:=5, Criteria1:="="
    Rows("2:2").Select
    ActiveWindow.ScrollRow = 85
    ActiveWindow.ScrollRow = 1011
    ActiveWindow.ScrollRow = 2275
    ActiveWindow.ScrollRow = 4381
    ActiveWindow.ScrollRow = 6656
    ActiveWindow.ScrollRow = 11121
    ActiveWindow.ScrollRow = 13311
    ActiveWindow.ScrollRow = 15923
    ActiveWindow.SmallScroll Down:=48
    Rows("2:99999").Select
    Selection.Delete Shift:=xlUp
    Selection.AutoFilter
    Range("C:C,D:D,F:F,G:G").Select
    Range("G1").Activate
    Selection.Delete Shift:=xlToLeft
    Range("C:C,D:D,F:F,G:G").EntireColumn.AutoFit
    Columns("D:D").Select
    Selection.NumberFormat = "[$-en-IN,1]yyyy/mm/dd;@"
```
## Generate UUID in excel for CAPM
Use the following formula to generate a UUID for CAPM
```sh
=CONCATENATE(DEC2HEX(RANDBETWEEN(0,4294967295),8),"-",DEC2HEX(RANDBETWEEN(0,42949),4),"-",DEC2HEX(RANDBETWEEN(0,42949),4),"-",DEC2HEX(RANDBETWEEN(0,42949),4),"-",DEC2HEX(RANDBETWEEN(0,4294967295),8),DEC2HEX(RANDBETWEEN(0,42949),4))
```