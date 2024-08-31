# i3 setup on Arch Linux


## Lightdm (Display manager)
```shell
pacman -S lightdm lightdm-gtk-greeter
systemctl enable lightdm
```

## i3 (Window manager)
```shell
pacman -S i3-wm rofi rofi-dmenu i3lock xss-lock
mkdir ~/.config/i3 && cp /etc/i3/config ~/.config/i3/config
# Modify config per need or use the one in the repo
```

## Picom (Compositor)
```shell
pacman -S picom
mkdir ~/.config/picom && cp /etc/xdg/picom.conf ~/.config/picom/picom.conf
# Modify config per need or use the one in the repo
touch ~/.picom.log


cat > ~/.config/picom/launch.sh << EOF
#!/bin/bash
killall -q picom
while pgrep -u $UID -x picom >/dev/null; do sleep 1; done
picom &
EOF

chmod a+x ~/.config/picom/launch.sh
```

## Rofi (Application launcher)
```shell
mkdir ~/.config/rofi && rofi -dump-config > ~/.config/rofi/config.rasii
vim ~/.config/rofi/config.rasii # Set the below value
    modi: "window,run,ssh,drun";
```

## Polybar (Status bar)
```shell
pacman -S xcb-proto
yay -S polybar
mkdir ~/.config/polybar && cp /usr/share/doc/polybar/config ~/.config/polybar/config
cat > ~/.config/polybar/launch.sh << EOF
#!/bin/bash
killall -q polybar
while pgrep -u $UID -x polybar >/dev/null; do sleep 1; done
polybar example &
EOF

chmod a+x ~/.config/polybar/launch.sh
```

## Feh (Image viewer)
```shell
pacman -S feh
```

## Applets (Network, Bluetooth)
```shell
pacman -S network-manager-applet
pacman -S blueman
```

## (If) After installing plymouth
```shell
systemctl disable lightdm
systemctl enable lightdm-plymouth
```

## Credits
1. https://i3wm.org/
1. https://github.com/blueman-project/blueman
1. https://github.com/derf/feh
1. https://github.com/canonical/lightdm
1. https://github.com/yshui/picom
1. https://github.com/polybar/polybar
1. https://github.com/davatorium/rofi
1. https://gitlab.gnome.org/GNOME/network-manager-applet
