## UFW Rules
    sudo ufw allow proto tcp from {client local IP} to any port 22,445 comment 'ssh, samba'
    sudo ufw allow proto tcp from {client local IP} to any port 8000,8834,8444 comment 'splunk, nessus, wazuh'

<br>

## Netplan
...

<br>

## SSH
- sshd_config:

        PermitRootLogin no
        MaxAuthTries 3
        PasswordAuthentication no

- PubkeyAuthentication only

<br>

## SMB
- smb.conf:

        [global]
            smb encrypt = required
            smb ports = 445
            hosts allow = {client local IP}
            hosts deny = 0.0.0.0/0
            security = user
            ntlmv2-only
            smb protocol = SMB3_11
            server min protocol = SMB3_11
            client min protocol = SMB3_11
            restrict anonymous = 2
            load printers = no
            disable spoolss = yes
            printing = bsd
    
        [{share name}]
           path = /home/{username}/{share folder path}
           browsable = no
           valid users = {username}



<br>

## Disabling Useless Services
    sudo systemctl stop cups cups-browsed && sudo systemctl disable cups cups-browsed
    sudo systemctl stop avahi-daemon.socket avahi-daemon && sudo systemctl disable avahi-daemon.socket avahi-daemon

## Crontab
    # Daily update
    0 0 * * * sudo apt-get update && sudo apt-get upgrade -y

    # Weekly backup
    0 4 * * 1 currdate=$(date "+%d/%m/%Y") && 7z a -snl /var/backups/homebkp-{$currdate}.7z /home/
