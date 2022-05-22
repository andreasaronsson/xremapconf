# xremapconf

https://github.com/k0kubun/xremap

## Arch linux

In order to be able to modify uinput first load the module.

`/etc/modules-load.d/uinput.conf`
```
uinput
```

Add a group.
```
sudo gpasswd -a <user> input
```

Then it is possible to add a udev rule.
`/etc/udev/rules.d/99-input.rules`

```
KERNEL=="uinput", GROUP="input", MODE="0660"
```

https://github.com/emberian/evdev/blob/1d020f11b283b0648427a2844b6b980f1a268221/src/scancodes.rs#L26-L572

`config.yml`

```
modmap:
  - name: aron
    remap:
      KEY_K: KEY_E
      KEY_E: KEY_J
      KEY_J: KEY_N
      KEY_N: KEY_K
      KEY_CAPSLOCK: KEY_LEFTCTRL
keymap:
  - name: Global
    remap:
      M_R-q: ALT_R-KEY_7
      M_R-w: ALT_R-KEY_8
      M_R-j: ALT_R-KEY_9
      M_R-r: ALT_R-KEY_0
      M_R-a: KEY_KPLEFTPAREN
      M_R-s: KEY_KPRIGHTPAREN
      M_R-d: KEY_KPSLASH
```

`~/.config/systemd/user/xremap.service`

```
[Unit]
Description=xremap

[Service]
Type=simple
Restart=always
ExecStart=xremap ~/.config/xremap/config.yml --watch

[Install]
WantedBy=default.target

```
