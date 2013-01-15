On linux / mac it is possible to access DBUS using https://npmjs.org/package/dbus-native.

method void org.gnome.ScreenSaver.Lock()
method void org.gnome.ScreenSaver.SetActive(bool value)
method void org.gnome.ScreenSaver.ShowMessage(QString summary, QString body, QString icon)
method void org.gnome.ScreenSaver.SimulateUserActivity()

method void org.gnome.SettingsDaemon.MediaKeys.GrabMediaPlayerKeys(QString application, uint time)

 qdbus --system org.freedesktop.UDisks /org/freedesktop/UDisks/devices/sda5 org.freedesktop.UDisks.Device.PartitionSize