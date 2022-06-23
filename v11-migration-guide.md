# Migrating to Mosaic React

## MUI Migrations guide

Read https://mui.com/guides/migration-v4/

## Upgrade dependencies

- Update React to 17.x
- Add `mosaic-react`
- Add new peer dependencies `@mui/material`, `@mui/lab`, `@mui/x-data-grid`,
  `@emotion/react`, and `@emotion/styled`
- If using icons, add `mosaic-react-icons` and `@mui/icons-material`
- Add `@mui/styles`, this will be removed later when updating to `emotion`
- Remove `s1-ui`, `s1-ui-icons`, and `s1-core-icons`
- Remove `@material-ui/core`, `@material-ui/icons`, `@material-ui/pickers`
- It is strongly recommended to replace `moment` with `date-fns`, see
  https://momentjs.com/docs/#/-project-status/

## Run code mod

- Run the `preset-safe` code mod on the root source folder, see
  https://mui.com/guides/migration-v4/#preset-safe

## Update import paths and names

- Replace `@mui/material` imports with `mosaic-react` imports. If using MUI
  components that are not included in mosaic-react, please let us know so that
  we can add them
- replace `s1-ui` imports with `mosaic-react`
- replace `s1-ui-icons` and `@mui/icons-material` imports with
  `mosaic-react-icons`. You will need to destructure the imports rather than
  using named files, for example `import Home from '@mui/icons-material/Home`
  becomes `import { Home } from 'mosaic-react-icons'`.
- `SovosFilterCheckboxList`, `SovosFilterTextEntry`, `SovosFilterDateInput`,
  `SovosDateRangePicker`, and `SovosNumberRangePicker` are no longer exported
  from '/sovos-filter-drawer'. Import these from the root index.
- `SovosDateRangePicker` is renamed `SovosFilterDateRange`
  `SovosNumberRangePicker` is renamed `SovosFilterNumberRange`, and
  `SovosFilterSection` is renamed `SovosFilterDrawerSection`
- `SovosFilterDrawer` is only a default export from '/sovos-filter-drawer'
- `SovosNotFoundPage` is renamed to `SovosErrorPage`
- `SovosContextSwitcher` renamed to `SovosAccountSwitcher`. This is likely not
  used directly, see updated props for `SovosGlobalLayout`

## Replace removed components

- `SovosTabCard__Deprecated`, replace with `SovosTabGroup`
- `SovosTableCard__Deprecated`, replace with `SovosTableGroup`
- `SovosAutoComplete__Deprecated`, replace with `SovosAutoComplete`
- `SovosAutoCompleteAsync__Deprecated`, replace with `SovosAutoComplete`
- `SovosNumberRangePicker`, use `SovosFilterNumberRange`
- `SovosDateRangePicker`, use `SovosFilterDateRange`
- `useWindowWidth`, use `useWindowSize`
- `useClickOutside` removed, use `ClickAwayListener`
- `SovosAttachmentsListTabIcon`, use Mui `AttachFile` icon, already the default
  in `SovosAttachmentsListTab`
- `SovosCommentsListTabIcon`, use Mui `ChatOutlined` icon, already the default
  in `SovosCommentsListTab`
- `SovosHistoryListTabIcon`, use Mui `DateRangeOutlined`, already the default in
  `SovosHistoryListTab`
- `SovosCloseButton`, replace with `SovosIconButton` with Mui `Close` icon
- `SovosChip`, replace with `SovosChipChoice`, `SovosChipFilter`, or
  `SovosChipInput`

## Remove components

- `SovosTreeListText__Deprecated`
- `SovosMenuContext`

## Remove/replace/add props

- `SovosConfirmationDialog` no longer takes children or the following other
  props: `defaultTitleText`, `defaultContentText`, `defaultActionButtonLabel`,
  `defaultCancelButtonLabel`. It takes `title` (required) and `content`
  (optional). `ActionButtonProps.children` is now required
- `SovosAttachmentsList`, remove `deleteButtonLabel` and `downloadButtonLabel`,
  they were ignored
- `SovosFilterDrawerSection` and `SovosFilterDateRange`, `addEnabled` and
  `removeEnabled` are removed, use `multiple`
- `SovosIconButton`, `ariaLabel` and `TooltipProps` props removed, use
  `tooltipText` which is now required.
- `SovosIconMenu`, `toolTipText` prop removed, use `tooltipText`
- `SovosEditableSlidingPanel`, `saveButtonLabel` is removed, use
  `SaveButtonProps`
- `SovosLink`, `text` prop removed, use `children`
- `SovosPaginationFooter`, `onPageChange` must now be a function. Passing in an
  object with `onNextClicked`, `onPerPageChanged`, `onPrevClicked`, and
  `onDirectPageChanged` is removed.
- `SovosEditableSlidingPanel`, remove `DialogTitleProps` and
  `DialogContentProps` from `CloseDialogProps` and replace with `title` and
  `content`.
- `SovosColumnDrawer`, remove `applyButtonLabel` and `cancelButtonLabel`, use
  `ApplyButtonProps.children` and `CancelButtonProps.children`.
- `SovosCommentForm`, `submitButtonLabel` prop is removed, us
  `submitButtonTooltipText`
- `SovosInputAdornment` now requires a `position` prop.
- `SovosToolbarSpace` no longer renders children, replace with
  `SovosToolbarGroup` if rendering child components
- `SovosErrorPage`, `errorCode` is a new required prop. `appName` is removed.
- `SovosGlobalLayout`, `navigationProps` shape changes
  - `contexts` renamed to `accounts`
    - `nestedContexts` renamed to `nestedAccounts`
    - `nestedContextCount` renamed to `nestedAccountCount`
  - `selectedContext` renamed to `selectedAccount`
  - `setContext` renamed to `setAccount`
  - `onExpandContext` renamed to `onExpandAccount`
  - `didContextChange` renamed to `didAccountChange`
- `SovosNavigation` props renamed to match those in `SovosGlobalLayout`

## Update date picker use

SovosDatePicker is rewritten to use the new @mui/lab DatePicker. To quote from
the migration guide:

> There are many changes, be careful, make sure your tests, and build pass. In
> the event you have an advanced usage of the date picker, it will likely be
> simpler to rewrite it.

There will be behavior changes:

- `onChange` no longer returns a faux event, but just a single value. The value
  will be a formatted string when valid, null if empty, and undefined if
  invalid. onChange will be fired anytime a valid value is in the field, and
  when the input is blurred
- The initial value passed into an empty date picker should not be undefined.
  Use null
- The format prop now uses unicode date strings. For example, 'YYYY-MM-DD'
  becomes 'yyyy-MM-dd'
- If using a format other than 'MM/dd/yyyy' or 'dd/MM/yyyy', you must set the
  `mask` property to match
- The new prop `TextFieldProps` should get props intended for the
  SovosTextField. This includes but is not size, fullWidth, style, helperText,
  error, etc. TextFieldProps.inputProps should receive props like placeholder,
  onFocus, onBlur, and aria-label, intended for the underlying input.

## Use new MUI API's

- `Grid` can use CSS attributes directly rather than specialized API, i.e. use
  `justifyContent` instead of `justify`
- `Grid` item spacing has changed significantly. Rather than padding on all
  sides, padding is now applied to the left and top of each item. Layouts will
  change as a result. Grid container margins may need to be adjusted to match.

## Fix breaking tests

- Wrap tests with a utility function that renders the component under test as a
  child of `SovosProvider` since components now require a theme and root level
  `ThemeProvider`. For example, the test wrapper looks something like this:

  ```javascript
  import React from 'react';
  import { render } from '@testing-library/react';
  import { SovosProvider } from 'mosaic-react';

  const renderWithProvider = (component) =>
    render(<SovosProvider theme={createTheme()}>{component}</SovosProvider>);

  export default renderWithProvider;
  ```

  and is used in tests like this:

  ```javascript
  import React from 'react';
  import { renderWithProvider } from 'testUtilities';
  import MyComponent from '.';

  const renderComponent = (props) =>
    renderWithProvider(
      <MyComponent {...props}>
        <span>Hi</span>
      </MyComponent>
    );

  describe('MyComponent', () => {
    it('should render without throwing any errors', () => {
      expect(() => renderComponent({ title: 'roar!' })).not.toThrow();
    });
  });
  ```

- Tests that search for elements by tooltip text need to use Testing Library's
  `getByLabelText` function rather `getByTitle`. Tooltips are implemented with
  an `aria-label` attribute instead of a `title` attribute.

## Theme updates

- The `spacing` function now returns a string with a `px` suffix. Remove the
  suffix before using in calculations

## Replace JSS with Emotion

- Follow steps in the MUI migration guide
  https://mui.com/guides/migration-v4/#migrate-from-jss
- Be sure to use the correct `styled` function. Import `styled` with
  `import { styled } from '@mui/material/styles';`
- Replace array values with strings, this is mostly for `padding` and `margin`
  shortcuts
- Replace function values with `props` in the function are to `styled`, see
  https://mui.com/customization/how-to-customize/#dynamic-css
- Replace `StylesProvider` and `createGenerateClassName` with the new, unstable
  `ClassNameGenerator`, see https://mui.com/guides/classname-generator/
- Remove `@mui/styles` from dependencies
- Basic rule for usage of `styled` vs. `sx` prop is to use `styled` when a style
  will be reused and to use `sx` when the style is a one off
