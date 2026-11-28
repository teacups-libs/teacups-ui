# Okisioli.Teacups.UI.Controls.Avalonia

Reusable Avalonia control styles.

## Root view

Use `RootView` as the app shell. Set `MainContent` to your app view or to a `DrawerSheet` that wraps the app's `NavigationPage` and hosts app-wide dialogs. The shell places separate snackbar and toast layers above `MainContent`.

```xml
<controls:RootView xmlns="https://github.com/avaloniaui"
                   xmlns:controls="clr-namespace:Okisioli.Teacups.UI.Controls.Avalonia;assembly=Okisioli.Teacups.UI.Controls.Avalonia">
  <controls:RootView.MainContent>
    <TextBlock Text="App content" />
  </controls:RootView.MainContent>
</controls:RootView>
```

See the [Avalonia demo startup](../../demo/Okisioli.Teacups.UI.Demo.Avalonia/App.axaml.cs) for the shell with dialog and popup services.

## Drawer sheet

`DrawerSheet` overlays optional `SheetContent` and scrolls it when it exceeds the available space.

```xml
<controls:DrawerSheet xmlns:controls="clr-namespace:Okisioli.Teacups.UI.Controls.Avalonia;assembly=Okisioli.Teacups.UI.Controls.Avalonia"
                      SheetVerticalAlignment="Bottom"
                      IsExpanded="{Binding IsSomethingOpen}">
  <controls:DrawerSheet.SheetContent>
    <SomeArbitraryControl />
  </controls:DrawerSheet.SheetContent>

  <MainPageContent />
</controls:DrawerSheet>
```

Both axes stretch by default. The example uses `SheetVerticalAlignment="Bottom"` to keep the sheet at the bottom and size its height to its content. Set `Placement` to choose the slide direction.

## Circular progress bar

Import the style dictionary in your application resources:

```xml
<StyleInclude Source="avares://Okisioli.Teacups.UI.Controls.Avalonia/Themes/CircularProgressBar.axaml" />
```

Then apply the `circular` class to an ordinary `ProgressBar`. The ring uses `Foreground` for the filled part and `Background` for the empty part.

```xml
<ProgressBar xmlns:controls="clr-namespace:Okisioli.Teacups.UI.Controls.Avalonia;assembly=Okisioli.Teacups.UI.Controls.Avalonia"
             Classes="circular"
             Width="160"
             Height="160"
             Minimum="0"
             Maximum="100"
             Value="64"
             Foreground="DodgerBlue"
             Background="#303030"
             controls:CircularProgress.RingThickness="12"
             controls:CircularProgress.Reverse="False" />
```

`RingThickness` is measured in device-independent pixels. The style fits the circle inside the shortest control dimension.
Set `CircularProgress.Reverse` to `True` to make the filled portion grow counter-clockwise.

## Gamepad button

`GamepadButton` offers three choices in one control. Click or tap to confirm the center choice, or press and drag left or right, then release to confirm a side. To cancel, drag upward and release, or press Escape during the gesture.

```xml
<controls:GamepadButton xmlns:controls="clr-namespace:Okisioli.Teacups.UI.Controls.Avalonia;assembly=Okisioli.Teacups.UI.Controls.Avalonia"
                        Confirmed="OnGamepadConfirmed" />
```

In the view's code-behind, give `OnGamepadConfirmed` the signature `void OnGamepadConfirmed(object? sender, GamepadButtonConfirmedEventArgs e)`. Use `e.Selection` to handle `GamepadButtonSelection.Left`, `Center`, or `Right`. Subscribe to `Cancelled` if the view needs to respond to a cancelled gesture.

Set `CenterBrush`, `LeftBrush`, and `RightBrush` to customize the choice colors.
