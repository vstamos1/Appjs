

|                  |     windows      |  Linux            |      mac         |
|------------------|------------------|-------------------|------------------|
| (interface)      |  SetWindowLong   |  `gtk_window_`    |  NSWindow, setStyleMask     |
| maximize-btn     | WS_MAXIMIZEBOX   |                   |                  |
| minimize-btn     | WS_MINIMIZEBOX   |                   |  NSMiniaturizableWindowMask  |
| icon             | WS_SYSMENU       |                   |                  |
| resizable        | WS_SIZEBOX       |     resizable     |  NSResizableWindowMask    |
| border           | WS_BORDER        |                   |   NSBorderlessWindowMask    |
| title-bar        | WS_CAPTION       |                   |  NSTitledWindowMask     |
| always-on-top    | WS_EX_TOPMOST    |  keep_above       | setLevel(orderFrontRegardless)  |
| floating-window  | WS_EX_TOOLWINDOW |                   | NSFloatingWindowLevel   |
| show-in-taskbar  | WS_EX_APPWINDOW  | skip_taskbar_hint |                  |
| disabled         | WS_DISABLED      |                   | ignoresMouseEvents  |
| visible          | WS_VISIBLE       |                   |  isVisible   |
| minimized        | WS_MINIMIZE      |                   |  isMiniaturized   |
| maximized        | WS_MAXIMIZE      |                   |                  |
| movable          |                  |                   |  isMovable        |
| fullscreen       | custom function  |   fullscreen      |  NSFullScreenWindowMask |
| alpha    | alpha, DWM func  |   [StackOverflow](http://stackoverflow.com/questions/3908565/how-to-make-gtk-window-background-transparent)|                  |

NSClosableWindowMask