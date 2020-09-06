# Macro related tips and tricks


- [Macro related tips and tricks](#macro-related-tips-and-tricks)
  - [Delete all empty rows](#delete-all-empty-rows)
  - [Delete row on empty column](#delete-row-on-empty-column)
  - [Get last row](#get-last-row)
  - [Format Date](#format-date)
  - [Check if worksheet is already available](#check-if-worksheet-is-already-available)
  - [Open Excel file dialog](#open-excel-file-dialog)
  - [Save file as txt](#save-file-as-txt)
  - [Application Parameters Enable / Disable](#application-parameters-enable--disable)
  - [Macro to get data from AMFI Portal](#macro-to-get-data-from-amfi-portal)
  - [Adjust rows macro](#adjust-rows-macro)

## Delete all empty rows
```sh
Sub DeleteAllEmptyRows()
    Dim LastRowIndex As Integer
    Dim RowIndex As Integer
    Dim UsedRng As Range
 
    Set UsedRng = ActiveSheet.UsedRange
    LastRowIndex = UsedRng.Row - 1 + UsedRng.Rows.Count
    Application.ScreenUpdating = False
 
    For RowIndex = LastRowIndex To 1 Step -1
        If Application.CountA(Rows(RowIndex)) = 0 Then
            Rows(RowIndex).Delete
        End If
    Next RowIndex
 
    Application.ScreenUpdating = True
End Sub
```
## Delete row on empty column
```sh
Sub DeleteRowEmptyColumn()
Application.ScreenUpdating = False
Columns("B:B").SpecialCells(xlCellTypeBlanks).EntireRow.Delete
Application.ScreenUpdating = True
```sh

## Open and close workbook
```sh
Workbooks.Open (fileName)

Workbooks(<<insert filename>>).Close
```
## Get last row
```sh
'Get Last row
lr = amcws.Cells(Rows.Count, "A").End(xlUp).Row
```

## Format Date
```sh
Format(<Insert worksheet name>.Range("<insert range of cell>").Value, "dd-mmm-yyyy")
```

## Check if worksheet is already available
```sh
'***********************************************************************************************************'
' Check if a worksheet is already available
'***********************************************************************************************************'

    HasByName = False
    Dim wb

    If oWorkBook Is Nothing Then
        Set oWorkBook = ThisWorkbook
    End If

    For Each wb In oWorkBook.Worksheets
        If wb.Name = cSheetName Then
            HasByName = True
            Exit Function
        End If
    Next wb
```
## Open Excel file dialog
```sh
Set fd = Application.FileDialog(msoFileDialogFilePicker)

  With fd
    .AllowMultiSelect = False
    .Title = "Please select the file."
    .Filters.Clear
    .Filters.Add "Excel 2003", "*.xls?"

    If .Show = True Then
      fileName = Dir(.SelectedItems(1))

    End If
  End With
```
## Save file as txt
```sh
 Dim xRet As Long
    Dim xFileName As Variant
    xFileName = Application.GetSaveAsFilename(Filename, "TXT File (*.txt), *.txt")
   
    ActiveSheet.Copy
    ActiveWorkbook.SaveAs xFileName, xlTextMSDOS
    If ActiveWorkbook.Name <> ThisWorkbook.Name Then
        ActiveWorkbook.Close False
    End If
```
## Application Parameters Enable / Disable
```sh
Application.DisplayAlerts = False
Application.ScreenUpdating = False
Application.EnableEvents = False

Application.StatusBar = <<<Insert required info for status bar>>
```

## Macro to get data from AMFI Portal
```sh
'Get Data from portal
With ActiveSheet.QueryTables.Add(Connection:= _
        "URL;http://portal.amfiindia.com/DownloadNAVHistoryReport_Po.aspx?" & url & "" _
        , Destination:=Range("$A$1"))
        .Name = _
        "abc"""
        .FieldNames = True
        .RowNumbers = False
        .FillAdjacentFormulas = False
        .PreserveFormatting = True
        .RefreshOnFileOpen = False
        .BackgroundQuery = True
        .RefreshStyle = xlInsertDeleteCells
        .SavePassword = False
        .SaveData = True
        .AdjustColumnWidth = True
        .RefreshPeriod = 0
        .WebSelectionType = xlEntirePage
        .WebFormatting = xlWebFormattingNone
        .WebPreFormattedTextToColumns = False
        .WebConsecutiveDelimitersAsOne = True
        .WebSingleBlockTextImport = False
        .WebDisableDateRecognition = False
        .WebDisableRedirections = False
        .Refresh BackgroundQuery:=False
    End With
```

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