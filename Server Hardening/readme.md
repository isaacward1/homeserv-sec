## UFW Rules
...

<br>

## Netplan
...

<br>

## SSH
- set PermitRootLogin no
- set PasswordAuthentication no

<br>

## SMB
...

<br>

## Disabling Useless Services
    sudo systemctl stop cups cups-browsed && sudo systemctl disable cups cups-browsed
    sudo systemctl stop avahi-daemon.socket avahi-daemon && sudo systemctl disable avahi-daemon.socket avahi-daemon

## Crontab
    # Daily update
    0 0 * * * sudo apt-get update && sudo apt-get upgrade -y

    # Weekly backup
    currdate=$(date "+%d/%m/%Y")
    0 4 * * 1 7z a -snl /var/backups/homebkp-[$currdate].7z /home/
