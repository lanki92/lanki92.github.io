
# Raspberry Pi - video kiosk

1. Write Raspbian image to SD Card / USB with Raspberry Pi Imager [Ubuntu x86](https://downloads.raspberrypi.org/imager/imager_latest_amd64.deb) / [Windows](https://downloads.raspberrypi.org/imager/imager_latest.exe), allow SSH and connect to Raspberry through [Putty](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe)

1. Create file ~/startup and make it executable

    ```
    echo -e "#!/bin/sh\nvlc $HOME/Desktop/top.mp4 --loop --qt-minimal-view --no-osd --fullscreen & sleep 2 && xdotool search --onlyvisible --class vlc windowmove 0 0\nvlc $HOME/Desktop/bottom.mp4 --loop --qt-minimal-view --no-osd --fullscreen & sleep 2 && xdotool search --onlyvisible --class vlc windowmove 2560 0" >> startup
    chmod +x startup
    ```

1. Create file ~/.config/autostart/autovlc.desktop and make it executable

    ```
    cd .config/autostart/
    echo -e "[Desktop Entry]\nType=Application\nExec=$HOME/startup" >> autovlc.desktop
    chmod +x autovlc.desktop
    ```

1. Copy 2 video file from Windows command line
 
    ```
    scp <local_file_to_upload> <current_rpi_username>@<rpi_ip_address>:<rpi_target_folder>
    ```

1. Disable wayland back to X11 and reboot (Advanced Options -> Wayland -> X11)
    ```
    sudo raspi-config
    ```
