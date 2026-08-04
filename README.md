<!-- default badges list -->
![](https://img.shields.io/endpoint?url=https://codecentral.devexpress.com/api/v1/VersionRange/1316050922/25.2.3%2B)
[![](https://img.shields.io/badge/Open_in_DevExpress_Support_Center-FF7200?style=flat-square&logo=DevExpress&logoColor=white)](https://supportcenter.devexpress.com/ticket/details/T1333061)
[![](https://img.shields.io/badge/📖_How_to_use_DevExpress_Examples-e9f6fc?style=flat-square)](https://docs.devexpress.com/GeneralInformation/403183)
[![](https://img.shields.io/badge/💬_Leave_Feedback-feecdd?style=flat-square)](#does-this-example-address-your-development-requirementsobjectives)
<!-- default badges end -->

# WPF ComboBoxEdit — Add a "Show More" Button to Reveal All Selected Tokens

This example attaches a reusable behavior to our WPF [ComboBoxEdit](https://docs.devexpress.com/WPF/DevExpress.Xpf.Editors.ComboBoxEdit). It displays selected items as tokens. If selected tokens do not fit within the editor's input box, the behavior displays a **Show More**/**Show Less** toggle button that expands or collapses the editor.

![WPF ComboBoxEdit with a Show More button, DevExpress](Images/show-more-button.png)

## Overview

The WPF `ComboBoxEdit` control in this example uses [CheckedTokenComboBoxStyleSettings](https://docs.devexpress.com/WPF/DevExpress.Xpf.Editors.CheckedTokenComboBoxStyleSettings) to render selected values as tokens. If tokens do not fit within the input box, the editor increases its height and displays a scrollbar by default. The `ShowMoreBehavior` provides an alternative user experience: it maintains editor height (fixed) and displays a toggle button allowing users to display all tokens on demand.

The `ShowMoreBehavior` is both self-contained and MVVM-friendly. You can attach it to any token-based `ComboBoxEdit` and set `CollapsedHeight`:

```xml
<dxe:ComboBoxEdit ItemsSource="{Binding AvailableRoles}"
                  EditValue="{Binding CurrentEmployee.RoleIds}"
                  DisplayMember="Name" ValueMember="Id">
    <dxmvvm:Interaction.Behaviors>
        <local:ShowMoreBehavior CollapsedHeight="22"/>
    </dxmvvm:Interaction.Behaviors>
</dxe:ComboBoxEdit>
```

## Implementation Details

The core logic is implemented in [ShowMoreBehavior.cs](./CS/ShowMoreBehavior.cs). The class modifies the following:

- **Token wrapping** — applies `CheckedTokenComboBoxStyleSettings` and enables `EnableTokenWrapping` to display selected values as tokens arranged across multiple lines.
- **Show More/Show Less button** — adds an editor button to `ComboBoxEdit.Buttons`. The button toggles editor height (`ComboBoxEdit.MaxHeight`) and its own caption between "Show More" and "Show Less".
- **Button visibility** — binds the inner `ScrollViewer.ScrollableHeight` and displays the button only when tokens overflow the collapsed editor (`ScrollableHeight > 0`) or the editor is expanded.

### Files to Review

- [ShowMoreBehavior.cs](./CS/ShowMoreBehavior.cs)
- [MainWindow.xaml](./CS/MainWindow.xaml)
- [MainViewModel.cs](./CS/MainViewModel.cs)
- [Employee.cs](./CS/Employee.cs)
- [EmployeeRole.cs](./CS/EmployeeRole.cs)

## Documentation

- [ComboBoxEdit](https://docs.devexpress.com/WPF/DevExpress.Xpf.Editors.ComboBoxEdit)
- [ComboBoxEdit Operation Modes (Token / Checked Token)](https://docs.devexpress.com/WPF/116528/controls-and-libraries/data-editors/common-features/editor-operation-modes/comboboxedit#checked-token-combobox)
- [CheckedTokenComboBoxStyleSettings](https://docs.devexpress.com/WPF/DevExpress.Xpf.Editors.CheckedTokenComboBoxStyleSettings)
- [ButtonInfo](https://docs.devexpress.com/WPF/DevExpress.Xpf.Editors.ButtonInfo)
- [Behaviors (DevExpress MVVM)](https://docs.devexpress.com/WPF/17442/mvvm-framework/behaviors)
<!-- feedback -->
## Does This Example Address Your Development Requirements/Objectives?

[<img src="https://www.devexpress.com/support/examples/i/yes-button.svg"/>](https://www.devexpress.com/support/examples/survey.xml?utm_source=github&utm_campaign=wpf-support-showmore-button-in-comboboxedit-with-tokens&~~~was_helpful=yes) [<img src="https://www.devexpress.com/support/examples/i/no-button.svg"/>](https://www.devexpress.com/support/examples/survey.xml?utm_source=github&utm_campaign=wpf-support-showmore-button-in-comboboxedit-with-tokens&~~~was_helpful=no)

(you will be redirected to DevExpress.com to submit your response)
<!-- feedback end -->
