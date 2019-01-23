Desktop Entry in Ubuntu
=======================
Explaining Desktop Entry aka Desktop icon in Ubuntu.


A Desktop entry or Desktop icon or Desktop shortcut or a Deshboard icon is all the same for Ubuntu which is a ``.desktop`` file. Follows is a example ``.desktop`` file contains::

    [Desktop Entry]
    Version=1.0
    Type=Application
    Terminal=false
    Name=$application_name
    GenericName=$generic_name
    Comment=$comment
    Path=$/path/to/working/directory
    Exec=$/path/to/excutable/file
    Icon=$/path/to/icon
    Categories=$categort_1,$categort_2
    StartupNotify=true

.desktop files can be found at the following directories in Ubuntu

- `/usr/share/applications/`
- `~/.local/share/applications`
- `/usr/local/share/applications`

Source
------
- `How can I find *.desktop files? <https://askubuntu.com/questions/117341/how-can-i-find-desktop-files>`_
- `Desktop files: putting your application in the desktop menu <https://developer.gnome.org/integration-guide/stable/desktop-files.html.en>`_
- `Desktop Entry Specification <https://standards.freedesktop.org/desktop-entry-spec/latest/index.html>`_
