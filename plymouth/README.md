Source [ArchWiki](https://wiki.archlinux.org/index.php/Plymouth)

- install `plymouth` and `plymouth-theme-arch-beat` with your AUR helper.
- add the `plymouth` HOOK to `/etc/mkinitcpio.conf` after base and udev  
- If you have full disk encryption like me replace the `encrypt` HOOK with `plymouth-encrypt` too.  

My HOOKS line:
```
HOOKS=(base udev plymouth autodetect modconf block keyboard keymap plymouth-encrypt lvm2 resume filesystems keyboard fsck shutdown suspend)
```
- add your display driver to MODULES. E.g. for Intel: `MODULES=(i915 [...])`
- run `mkinitcpio -p linux`
- Add `quiet splash loglevel=3 rd.udev.log_priority=3 vt.global_cursor_default=0` to your kernel parameters
- change `/etc/plymouth/plymouthd.conf` to
```
[Daemon]
Theme=arch-beat
ShowDelay=5
DeviceTimeout=5
``` 
- run `sudo plymouth-set-default-theme -R arch-beat` to apply theme
- For smooth transition disable your display manager unit e.g. `lightdm.service`   
  and enable the respective DM-plymouth unit e.g. `lightdm-plymouth.service`
