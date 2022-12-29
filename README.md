## auto-ytdlp

This is an auto downloader script for multiple youtube channels or playlists.
You can track and automatically download content from creators that you want to follow.

When run, by default it will check for any videos you have not already downloaded within the last five days and download them for you in the directories you specify. Each playlist or Channel will have it's own directories, which you can specify.

I am uploading this for my own benefit, you are free to use and modify it as you see fit.
I may eventually make this more user friendly.

I have recently made it harder to break the application by fixing bugs. If you find any bugs or think of ways this can be improved, Please don't hesistate to raise an issue.

## Directions


This script requires yt-dlp you can install for your distro or get it here: https://github.com/yt-dlp/yt-dlp


```git clone https://github.com/exadisme/auto-ytdlp.git```

```cd auto-ytdlp```

Make it executable: ```chmod +x auto-ytdlp```

Place files somewhere within your path or add the folder to your path variable. All files need to be together for this to work.


```
Usage:
     auto-ytdlp                                 Will check for youtube video updates and download them.
     auto-ytdlp [options]

Options:
     --help                                     Shows this menu.
     -l                                         List all currently added channels.
     -a URL SaveDirectory Name of the channel   Add a channel or playlist.
     -d <number>                                Delete a channel. Get the number from list.
     -u <number>                                Change how far back, in days, the script looks for new videos. Default is 5 days back.
     -p <number>                                Change how many videos in the playlist yt-dlp will check the dates of. Higher value can increase the time it takes to fetch videos, Lower values may cause you to miss videos if content is uploaded often. Default is 10.
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
then you could ```sudo systemctl enable youtube_download.service --now```
