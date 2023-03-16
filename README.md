# Claim your Linux Plex server from the shell

## Introduction

The Plex Media Server setup requires you to link your new server to your plex.tv account. This is done by initially accessing your server from "the same network" [1]. This can be a little "complicated" on a remote headless server if you have never heard of an "ssh tunnel" before.

The script in this git repo just uses the same mechanics that are used by the official Plex Docker image [2]. In fact, the script is just a refactored version of the Docker script.

## Synology usage as 3/16/2023
 1. Enable SSH and connect to your server
 2. Take note of your volume names, I only had one named `volume1` but yours may be different.
 3. `cd /volume1/PlexMediaServer` Replace volume 1 with your volume name that contains the PlexMediaServer folder
  - NOTE: There may be an old `Plex` folder in `volume1`, this is no longer used after an update sometime in 2022.
 4. `wget https://raw.githubusercontent.com/blueal/plex-claim-server-synology/master/plex-claim-server.sh`
 5. IF your volume is anything other then `volume1`, you will need to open the file in vi and edit the first variable. Otherwise you may skip this step
  - `vi plex-claim-server.sh`
  - edit the `volumeName` variable at the top of page to match your volume name, such as `volume2` or whatever it might be.
  - To edit: press `i` arrow key over to the variable, and edit the name. Press the `esc` key, then type `:wq`.
 6. `chmod +x plex-claim-server.sh`
 7. Get your Plex Claim Code (it's only valid for 4 minutes): https://www.plex.tv/claim/
 8. Claim your server: `sudo -u plex ./plex-claim-server.sh "$YOUR_CLAIM_CODE"
    - You may be asked to type in your password, and given a warning. This is normal.
 9. This is only succesfull if there were NO errors (such as file not found) and it says "Plex Media Server succesfully claimed".
 10. Restart Plex in package center
 11. `rm plex-claim-server.sh`

## Usage

1. ~~Make the script executable: `chmod +x plex-claim-server.sh`~~  
2. ~~Get your Plex Claim Code (it's only valid some minutes): https://www.plex.tv/claim/~~  
3. ~~Claim your server: `sudo -u plex ./plex-claim-server.sh "$YOUR_CLAIM_CODE"`~~
4. ~~Restart your Plex Media Server, e.g. with `sudo systemctl restart plexmediaserver`~~


## ~~Advanced Usage~~

NOTE: I've disabled this just because it seemed easier. It can easily be added back by looking at the previous version.

~~Set the environment variable `PLEX_MEDIA_SERVER_APPLICATION_SUPPORT_DIR` to tell the script about your non-default Plex setup.~~

[1] https://support.plex.tv/articles/200288586-installation/#toc-2

[2] https://github.com/plexinc/pms-docker

