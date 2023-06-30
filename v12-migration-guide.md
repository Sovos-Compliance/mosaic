# Migrating to Mosaic React v12

## MUI X Migrations guides

Data Grid: https://mui.com/x/migration/migration-data-grid-v5/<br> Date Picker:
https://mui.com/x/migration/migration-pickers-v5/

## Run codemods

<p>
  // Date and Time Pickers specific<br/>
  <code>npx @mui/x-codemod v6.0.0/pickers/preset-safe <path></code>
</p>

<p>
  // Data Grid specific<br />
  <code>npx @mui/x-codemod v6.0.0/data-grid/preset-safe <path></code>
</p>

## Rename SovosDataGrid Props

To avoid confusion with the props that will be added for the cell
selectionfeature, some props related to row selection were renamed to have "row"
in their name. The renamed props are the following: 2023-05-16

<table>
  <thead>
  <tr>
  <th align="left">Old name</th>
  <th align="left">New name</th>
  </tr>
  </thead>
  <tbody><tr>
  <td align="left"><code>selectionModel</code></td>
  <td align="left"><code>rowSelectionModel</code></td>
  </tr>
  <tr>
  <td align="left"><code>onSelectionModelChange</code></td>
  <td align="left"><code>onRowSelectionModelChange</code></td>
  </tr>
  <tr>
  <td align="left"><code>disableSelectionOnClick</code></td>
  <td align="left"><code>disableRowSelectionOnClick</code></td>
  </tr>
  <tr>
  <td align="left"><code>disableMultipleSelection</code></td>
  <td align="left"><code>disableMultipleRowSelection</code></td>
  </tr>
  <tr>
  <td align="left"><code>showCellRightBorder</code></td>
  <td align="left"><code>showCellVerticalBorder</code></td>
  </tr>
  <tr>
  <td align="left"><code>showColumnRightBorder</code></td>
  <td align="left"><code>showColumnVerticalBorder</code></td>
  </tr>
  <tr>
  <td align="left"><code>headerHeight</code></td>
  <td align="left"><code>columnHeaderHeight</code></td>
  </tr>
  </tbody>
</table>

Check the migration guide for any **Removed Props** you may be using:<br>
https://mui.com/x/migration/migration-data-grid-v5/#removed-props

## SovosDatePicker Props

MUI X v6 prop changes for the date picker have been mapped to existing props so
no changes should be required.
