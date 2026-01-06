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

Here you can download Bazzite - https://download.bazzite.gg/bazzite-deck-stable-live.iso

By default the GPU clock will always stay at 1500MHz. You may want to install a governor with these commands:

sudo copr enable filippor/bazzite

sudo rpm-ostree install oberon-governor

systemctl reboot

systemctl enable --now oberon-governor

Now the GPU clock will go up to 2000MHz. You can tune it by editing the following file:

/etc/oberon-config.yaml

You can set the max frequency to 2230MHz and the voltage 1129mV. My board overheated at 2230MHz so I went with 2100MHz and undervolted it a bit. After making the changes you need to type:

systemctl restart oberon-governor

To get more performance you can you the following command. You will get better performance but your board will be vulnerable to some well known exploits.

sudo rpm-ostree kargs --append-if-missing="mitigations=off"

You can increase the amount of ZRAM to 16GB  by editing the following file:

/etc/systemd/zram‑generator.conf

and set zram-size=16384

If you want to change the fan speed for the desktop you can instal coolercontrol with this command:

ujust install-coolercontrol
