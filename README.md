# How to clear sorting in a Flutter DataTable?

In this article, we will show you how to clear sorting in a [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with all the necessary properties. The [SfDataGrid.source.sortedColumns](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource/sortedColumns.html) collection contains the sorted columns. By clearing this collection, you can remove the sorting applied to the DataGrid. We have outlined three methods for clearing the sorting in various scenarios.

* Clear all sorted columns from the DataGrid.
```dart
employeeDataSource.sortedColumns.clear();
```
* Retain sorting on the respective column and remove sorting from the remaining columns.
```dart
employeeDataSource.sortedColumns.removeWhere((column) => column.name != 'name');
```
* Retain only the last sorted column and clear the remaining columns.
```dart
employeeDataSource.sortedColumns.retainWhere((column) => column == employeeDataSource.sortedColumns.last);
```

* Sample
```dart
@override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Syncfusion Flutter DataGrid'),
      ),
      body: Column(
        children: [
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              TextButton(
                  onPressed: () {
                    // Clicking the "clear sorting" button resets all sorting states,
                    // clearing the current sort order.
                    if (employeeDataSource.sortedColumns.isNotEmpty) {
                      employeeDataSource.sortedColumns.clear();
                      employeeDataSource.sort();
                    }
                  },
                  child: const Text('Clear sorting')),
            ],
          ),
          Expanded(
            child: SfDataGrid(
              source: employeeDataSource,
              columnWidthMode: ColumnWidthMode.fill,
              allowSorting: true,
              showSortNumbers: true,
              allowMultiColumnSorting: true,
              columns: <GridColumn>[
                GridColumn(
                    columnName: 'id',
                    label: Container(
                        padding: const EdgeInsets.all(16.0),
                        alignment: Alignment.center,
                        child: const Text(
                          'ID',
                        ))),
                GridColumn(
                    columnName: 'name',
                    label: Container(
                        padding: const EdgeInsets.all(8.0),
                        alignment: Alignment.center,
                        child: const Text('Name'))),
                GridColumn(
                    columnName: 'designation',
                    label: Container(
                        padding: const EdgeInsets.all(8.0),
                        alignment: Alignment.center,
                        child: const Text(
                          'Designation',
                          overflow: TextOverflow.ellipsis,
                        ))),
                GridColumn(
                    columnName: 'salary',
                    label: Container(
                        padding: const EdgeInsets.all(8.0),
                        alignment: Alignment.center,
                        child: const Text('Salary'))),
              ],
            ),
          ),
        ],
      ),
    );
}
```

You can download this example on [GitHub](https://github.com/SyncfusionExamples/How-to-clear-sorting-in-a-Flutter-DataTable).