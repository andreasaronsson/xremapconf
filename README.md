# xremapconf

https://github.com/k0kubun/xremap

## Arch linux sudo

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

```sh
modmap:
  - name: aron
    remap:
      KEY_F: KEY_T
      KEY_E: KEY_F
      KEY_T: KEY_G
      KEY_K: KEY_E
      KEY_N: KEY_K
      KEY_J: KEY_N
      KEY_G: KEY_D
      KEY_R: KEY_J
      KEY_S: KEY_R
      KEY_D: KEY_S      
      KEY_CAPSLOCK: KEY_LEFTCTRL
keymap:
  - name: Global
    remap:
      M_R-q: ALT_R-KEY_7
      M_R-w: ALT_R-KEY_8
      M_R-f: ALT_R-KEY_9
      M_R-j: ALT_R-KEY_0
      M_R-a: KEY_KPLEFTPAREN
      M_R-r: KEY_KPRIGHTPAREN
      M_R-s: KEY_KPSLASH
```

`~/.config/systemd/user/xremap.service`

```
[Unit]
Description=xremap
After=default.target

[Service]
Type=simple
Restart=always
ExecStart=xremap ~/.config/xremap/config.yml
ReStartSec=60
StartLimitInterval=30

[Install]
WantedBy=default.target

```
