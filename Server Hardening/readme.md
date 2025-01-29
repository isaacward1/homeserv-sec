## Firewall (ufw) Configuration

    Status: active
    Logging: off
    Default: deny (incoming), allow (outgoing), disabled (routed)
    New profiles: skip
    
    To                         Action      From
    --                         ------      ----
    192.168.1.0/24             DENY OUT    Anywhere                 # local isolation
    22,445/tcp                 ALLOW IN    192.168.1.X              # local ssh, smb
    8834/tcp                   ALLOW IN    192.168.1.X              # nessus
    8000/tcp                   ALLOW IN    192.168.1.X              # splunk
    1514,1515,8444/tcp         ALLOW IN    192.168.1.X              # wazuh

<br>

## Blacklist malicious IPs
    sudo apt install fail2ban
    sudo systemctl start fail2ban && sudo systemctl enable fail2ban


<br>

## Home folder encryption
    
    sudo apt-get install ecryptfs-utils cryptsetup
    sudo useradd -G sudo tempuser
    su tempuser
    sudo ecryptfs-migrate-home -u {username}
    exit
    sudo ecryptfs-setup-swap
    sudo rm -rf /home/{username}.*

<br>

## SSH
- sshd_config:

        PermitRootLogin no
        MaxAuthTries 3
        PasswordAuthentication no

- Public key auth:

      ssh-keygen -t rsa -b 4096
      ssh-copy-id {username}@{server IP}

      # on server
      sudo cp ~/.ssh/authorized_keys /etc/ssh/authorized_keys
      cd /etc/ssh/ && sudo chown {username}:{username} authorized_keys
        
<br>

## SMB
- smb.conf:

        [global]
            smb encrypt = required
            smb ports = 445
            hosts allow = {192.168.1.X}
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
    0 0 * * * sudo apt update && sudo apt upgrade && sudo apt autoremove --purge && sudo apt autoclean -y

    # Weekly backup
    0 4 * * 1 currdate=$(date "+%d/%m/%Y") && rm /var/backups/homebkp*.7z && 7z a -snl /var/backups/homebkp-{$currdate}.7z /home/
