# HomeExplorer — Windows 11 File Explorer Address Bar Home Button (Windhawk Mod)

A Windhawk C++ mod ([`explorer-home-button.wh.cpp`](explorer-home-button.wh.cpp)) for Windows 11 Pro (`explorer.exe`) that adds a dedicated **Home ("This PC")** button directly adjacent to the **Refresh** button in the modern WinUI 3 / XAML Islands File Explorer address bar.

## Features

- **Target Process**: `explorer.exe` on Windows 11 (supports builds with WinUI 3 / XAML Islands `FileExplorerExtensions.NavigationBarControl` and tabs).
- **Native WinUI 3 Look & Feel**:
  - Injects a `Microsoft.UI.Xaml.Controls.AppBarButton` directly into `CommandBar#NavigationCommands` next to `AppBarButton#refreshButton`.
  - Copies size, margins, padding, corner radius, focus visuals, and style from the native Refresh button.
  - Uses Segoe Fluent Icons Home (`\uE80F`) or Computer (`\uE770`) glyph matching `refreshButton`'s `FontIcon` metrics.
  - Dynamically adapts to Windows 11 **Light**, **Dark**, and **High Contrast** themes.
  - Default tooltip: `"This PC (Alt+Home)"`.
- **Active-Tab-Only Navigation**:
  - Uses COM Shell APIs (`IShellWindows`, `IServiceProvider`, `IShellBrowser::BrowseObject`, and `IWebBrowser2::Navigate2`) matched against the active `ShellTabWindowClass` child window so clicking the button navigates **only the currently active tab** in that File Explorer window to `shell:MyComputerFolder` (`::{20D04FE0-3AEA-1069-A2D8-08002B30309D}`).
- **Configurable Windhawk Settings**:
  - **Target Location**: Configurable shell URI, CLSID, or folder path (defaults to `shell:MyComputerFolder`).
  - **Button Placement**: Place `before` or `after` the Refresh button.
  - **Icon Glyph**: Choose between Home (`\uE80F`) and Computer / This PC (`\uE770`).
  - **Tooltip Text**: Customize the hover tooltip (defaults to `This PC (Alt+Home)`).
- **Clean Lifecycle**:
  - Supports dynamic injection into already-open File Explorer windows, live settings reloads (`Wh_ModSettingsChanged`), and clean uninitialization (`Wh_ModUninit`) without crashing or leaking XAML elements.

## Installation

1. Open **Windhawk** and click **Create a new mod** (bottom right) or edit an existing custom mod.
2. Paste the contents of [`explorer-home-button.wh.cpp`](explorer-home-button.wh.cpp) into the editor.
3. Click **Compile Mod** in Windhawk.
