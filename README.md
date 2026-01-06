# amd-bc250-steam-machine-guide
Guide for building a Steam Machine from an AMD BC‑250


Here is a link to a 3D printed case - https://www.thingiverse.com/thing:7165679

You may need to use tinkercad to enlarge the space for the PSU in the Shell_Back_FLEX_ATX.stl file depending on the PSU that you are using.

I have added to the repo a modfied Shell_Back_Dell.stl that Im using with a Dell server PSU

You will need a 400W PSU.

If you are going to use a Dell server PSU then you will need to make a cable for it and short pins S13, S14 and S16 on the PSU. I added a pinout diagram to the repo.

If you want to use the mentioned case, you will need to straighten the radfiator fins. You can print a tool for that - https://www.printables.com/model/1282906-bc-250-scooper or you can buy a fin straightening tool online

The mentioned case uses Arctic 12 pro fans for cooling. You can use one or two of those fans.


You will probably need dongles for wifi and bluetooth. Here the ones that Im using:

D-LINK DWA-181 - Wifi

TP-LINK UB500 Plus - BT

You will need an M.2 NVME 2280 SSD (the board supports PCIe 2.0)

sudo copr enable filippor/bazzite
sudo rpm-ostree install oberon-governor
systemctl reboot
systemctl enable --now oberon-governor

https://download.bazzite.gg/bazzite-deck-stable-live.iso

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
