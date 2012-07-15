|                  |     windows      |  Linux           |      mac         |
|                  |  SetWindowLong   |  gtk_window_     |                  |
|------------------|------------------|------------------|------------------|
| maximize-btn     | WS_MAXIMIZEBOX   |                  |                  |
| minimize-btn     | WS_MINIMIZEBOX   |                  |                  |
| icon             | WS_SYSMENU       |                  |                  |
| resizable        | WS_SIZEBOX       |     resizable    |                  |
| border           | WS_BORDER        |                  |                  |
| title-bar        | WS_CAPTION       |                  |                  |
| always-on-top    | WS_EX_TOPMOST    |  keep_above      |                  |
| floating-window  | WS_EX_TOOLWINDOW |                  |                  |
| show-in-taskbar  | WS_EX_APPWINDOW  | skip_taskbar_hint|                  |
| disabled         | WS_DISABLED      |                  |                  |
| visible          | WS_VISIBLE       |                  |                  |
| minimized        | WS_MINIMIZE      |                  |                  |
| maximized        | WS_MAXIMIZE      |                  |                  |
| fullscreen       | custom function  |   fullscreen     |                  |
| alpha/opacity    | alpha, DWM func  |   opacity        |                  |
