# Virt manager

# Persistently resize windows

Close the `Virt-Manager` main application window in order to for window geometry
changes to persist. (It is not sufficient to close only the VM window.)

Alternatively, when the UI is closed, you can also edit the dconf settings. In
`dconf-editor`, select the VM from `/org/virt-manager/virt-manager/vms/` and
edit the `vm-window-size` setting.
