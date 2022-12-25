## auto-ytdlp

This is an auto downloader script for multiple youtube channels or playlists.

When run, by default it will check for any videos you have not already downloaded within the last five days and download them for you in the directories you specify. Each playlist or Channel will have it's own directories.

I am uploading this for my own benefit, you are free to use and modify it as you see fit.
I may eventually make this more user friendly.

Currently, it is likely easy to break but I will be updating this to make it more userfriendly and error out if unexpected values are used. In the meantime, just be careful when inputing commands.

## Directions


This script requires yt-dlp you can install for your distro or get it here: https://github.com/yt-dlp/yt-dlp


```git clone https://github.com/exadisme/auto-ytdlp.git```

```cd auto-ytdlp```

Make it executable: ```chmod +x auto-ytdlp```

Place files somewhere within your path or add the folder to your path variable. All files need to be together for this to work.


```
Usage:
     auto-ytdlp                               Will check for youtube video updates and download them.
     auto-ytdlp [options]

Options:
     --help                                    Shows this menu.
     -l                                        List all currently added channels.
     -a URL SaveDirectory Name of the channel  Add a channel or playlist.
     -d <number>                               Delete a channel. Get the number from list.
```
## Running as a service systemd

If you wanted to set this up as a service you could create a systemd service with the following options:

```
[Unit]
Description=Youtube video downloader script
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
ExecStart=/bin/bash /path/to/script/auto-ytdlp
User=<your username>
Restart=on-failure
Environment="DISPLAY=:0" "XAUTHORITY=/home/<your username>/.Xauthority"

[Install]
WantedBy=multi-user.target
```
If you wanted it to run every 2 hours or so, you could also set up a .timer for the service like so:
```
[Unit]
Description=Run my youtube download script every 2 hours.

[Timer]
OnBootSec=5min
OnUnitActiveSec=2h
Unit=youtube_download.service

[Install]
WantedBy=multi-user.target
```
then you could sudo systemctl ```enable youtube_download.service --now```
