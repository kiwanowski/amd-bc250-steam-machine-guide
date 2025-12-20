# amd-bc250-steam-machine-guide
Guide for building a Steam Machine from an AMD BC‑250


https://www.thingiverse.com/thing:7165679
https://www.printables.com/model/1282906-bc-250-scooper

Arctic 12 pro

D-LINK DWA-181 - Wifi
ASUS USB-BT500 - bluetooth
TP-LINK UB500 Plus

sudo copr enable filippor/bazzite
sudo rpm-ostree install oberon-governor
systemctl reboot
systemctl enable --now oberon-governor

etc/oberon-config and restart the governor systemctl restart oberon-governor

sudo rpm-ostree kargs --append-if-missing="mitigations=off"

ujust install-coolercontrol

/etc/systemd/zram‑generator.conf

16384
