# amd-bc250-steam-machine-guide
Guide for building a Steam Machine from an AMD BC‑250


https://www.thingiverse.com/thing:7165679
https://www.printables.com/model/1282906-bc-250-scooper

Arctic 12 pro

D-LINK DWA-181 - Wifi
TP-LINK UB500 Plus - bt

sudo copr enable filippor/bazzite
sudo rpm-ostree install oberon-governor
systemctl reboot
systemctl enable --now oberon-governor

https://download.bazzite.gg/bazzite-deck-stable-live.iso

Dell server power supply

/etc/oberon-config.yaml

frequency:
max: 2100 #2230
voltage:
max: 950 #1129

gfx_temp_soft_lim: 95
gfx_temp_hard_lim: 95 
soc_temp_hard_lim: 95

systemctl restart oberon-governor

sudo rpm-ostree kargs --append-if-missing="mitigations=off"

ujust install-coolercontrol

/etc/systemd/zram‑generator.conf

zram-size=16384
