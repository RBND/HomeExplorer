# HomeExplorer — Windows 11 File Explorer Address Bar Home Button (Windhawk Mod)

A native Windhawk mod ([`explorer-home-button.wh.cpp`](explorer-home-button.wh.cpp)) for Windows 11 (`explorer.exe`) that adds a dedicated **Home ("This PC")** button directly adjacent to the **Refresh** button in the File Explorer address bar.

![File Explorer Address Bar Home Button](https://raw.githubusercontent.com/RBND/HomeExplorer/main/screenshot.png)

## Features

- **Native WinUI 3 Integration**:
  - Injects a `Microsoft.UI.Xaml.Controls.AppBarButton` directly into `CommandBar#NavigationCommands` next to `AppBarButton#refreshButton`.
  - Discovered cleanly via WinUI 3 symbol hooking in `FileExplorerExtensions.dll` without XAML Diagnostics (fully compatible with *Windows 11 File Explorer Styler* and *UWPSpy*).
  - Copies size, margins, padding, corner radius, focus visuals, and style from the native Refresh button.
  - Uses Segoe Fluent Icons Home (`\uE80F`) or Computer (`\uE770`) glyph matching `refreshButton`'s `FontIcon` metrics.
  - Dynamically inherits Windows 11 **Light**, **Dark**, and **High Contrast** themes.
- **Active-Tab-Only Navigation**:
  - Uses COM Shell APIs (`IShellWindows`, `IServiceProvider`, `IShellBrowser::BrowseObject`, and `IWebBrowser2::Navigate2`) matched against the active `ShellTabWindowClass` child window with fast HWND validation so clicking the button navigates **only the currently active tab** in that File Explorer window to `shell:MyComputerFolder` (`::{20D04FE0-3AEA-1069-A2D8-08002B30309D}`).
- **Configurable Windhawk Settings**:
  - **Target Location**: Configurable shell URI, CLSID, or folder path (defaults to `shell:MyComputerFolder`).
  - **Button Placement**: Place `before` or `after` the Refresh button.
  - **Icon Glyph**: Choose between Home (`\uE80F`) and Computer / This PC (`\uE770`).
  - **Tooltip Text**: Customize the hover tooltip and automation name (defaults to `This PC`).
- **Clean Lifecycle**:
  - Supports dynamic injection into already-open File Explorer windows, live settings reloads (`Wh_ModSettingsChanged`), and clean uninitialization (`Wh_ModUninit`) without crashing or leaking XAML elements.

## Installation

1. Open **Windhawk** and click **Create a new mod** (bottom right) or edit an existing custom mod.
2. Paste the contents of [`explorer-home-button.wh.cpp`](explorer-home-button.wh.cpp) into the editor.
3. Click **Compile Mod** in Windhawk.
