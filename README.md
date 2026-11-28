# Teacups UI

A (hopefully) growing collection of small, narrow-focused, **reusable UI building blocks and helpers for .NET apps**, initially focusing on Avalonia and WPF.

Stuff that I (and many of us) wrote many times over and over again. And even if today it's matter of seconds for an agent to write things like this, I don't want to repeat my prompts every time - I'd rather build my own foundation for every future project, and let it evolve over time.

👉 A sibling repository, focused on various non-UI functionality and helpers, can be found at [Teacups](https://github.com/okisioli/teacups).

🚀 Some useful hacks for **making WPF faster** live under the [Fastr.WPF](src/Okisioli.Teacups.UI.Fastr.WPF) package.

## Packages

| Package | Purpose |
| --- | --- |
| [Okisioli.Teacups.UI.Core](src/Okisioli.Teacups.UI.Core) | Framework-neutral UI service contracts. |
| [Okisioli.Teacups.UI.Core.WPF](src/Okisioli.Teacups.UI.Core.WPF) | WPF implementations of the Core dialog and UI dispatcher services. |
| [Okisioli.Teacups.UI.Core.Avalonia](src/Okisioli.Teacups.UI.Core.Avalonia) | Avalonia implementations of the Core dialog, popup, and UI dispatcher services. |
| [Okisioli.Teacups.UI.Controls.Avalonia](src/Okisioli.Teacups.UI.Controls.Avalonia) | Avalonia controls and styles.<ul><li>Expandable drawer sheet for dialogs and bottom sheets</li><li>Root view with toast and snackbar layers</li><li>Three-state floating action button</li><li>Circular progress bar</li></ul> |
| [Okisioli.Teacups.UI.Behaviors.Avalonia](src/Okisioli.Teacups.UI.Behaviors.Avalonia)<br>[Okisioli.Teacups.UI.Behaviors.WPF](src/Okisioli.Teacups.UI.Behaviors.WPF) | XAML interaction behaviors.<ul><li>Long press on any element</li><li>List item double-click commands</li><li>Text box submission and tag entry</li></ul> |
| [Okisioli.Teacups.UI.Fastr.WPF](src/Okisioli.Teacups.UI.Fastr.WPF) | Buffered item sources, incremental collection updates, and optional scroll resets for WPF item controls. |

## Usage

Use [`RootView`](src/Okisioli.Teacups.UI.Controls.Avalonia/README.md#root-view) as the shell for a new Avalonia app. Put your app view in `MainContent`. To add app-wide dialogs, wrap the app's `NavigationPage` in a dedicated `DrawerSheet` and use that sheet as `MainContent`. Individual pages can still use their own drawers. `RootView` adds an interactive snackbar layer and a passive toast layer above the app and its dialogs. Pass the root to `PopupService` to show toasts and snackbars. See the [Avalonia demo startup](demo/Okisioli.Teacups.UI.Demo.Avalonia/App.axaml.cs) for the wiring.

To build your own shell, layer the app content (or its dialog sheet), an interactive snackbar presenter, and a toast presenter with hit testing disabled in a `Grid`, in that order. A custom shell supplies its own popup wiring because `PopupService` takes a `RootView`.

For WPF and Avalonia, use the platform package's implementation of `IDispatcherService` to queue work on the UI thread and `IDialogService<TViewModel, TView>` to show a dialog for a view model and await whether it was accepted.

## Demos

- [WPF Controls](demo/Okisioli.Teacups.UI.Demo.WPF)
- [WPF Fastr](demo/Okisioli.Teacups.UI.Fastr.Demo.WPF) · Run the project on Windows with the .NET 10 SDK.
- [Avalonia](demo/Okisioli.Teacups.UI.Demo.Avalonia) · [View in browser](https://okisioli.github.io/teacups-ui/)

To run the Avalonia browser demo locally, install the .NET 10 SDK and run
`./start.ps1` in PowerShell. The script restores the required WebAssembly workload,
builds the demo, and prints the local URL. The [desktop host](demo/Okisioli.Teacups.UI.Demo.Avalonia.Desktop)
can be run from the solution.
