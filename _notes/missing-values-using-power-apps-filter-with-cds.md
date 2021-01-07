# Missing column values when using Filter() against Dataverse Table in Power Apps using CDS data source

Usually when you use the `Filter()` function against a data source in Power Apps, all columns and values are returned in the result.

However the CDS data source seems to act differently, consider the below expression to populate a collection using `Filter()`.

```js
ClearCollect(colMyCollection,
    Filter(myDataverseTable,ColumnName = "Value")
)
```

The collection will contain all columns from the table but not all of them will be populated, to return values from the non populated columns, we need to use the `ShowColumns()` function to specify the columns to be populated, using the `Filter()` as the data source.

```js
ShowColumns(
    ClearCollect(colMyCollection,
        Filter(myDataverseTable,ColumnName = "Value")
    ),
    ColumnName,
    ColumnName,
    ...
)
```
