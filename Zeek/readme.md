## Install

    echo 'deb http://download.opensuse.org/repositories/security:/zeek/xUbuntu_24.04/ /' | sudo tee /etc/apt/sources.list.d/security:zeek.list
    curl -fsSL https://download.opensuse.org/repositories/security:zeek/xUbuntu_24.04/Release.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/security_zeek.gpg > /dev/null
    sudo apt update
    sudo apt install zeek
    # No postfix configuration
    
<br>

## Config

    sudo echo PREFIX='/opt/zeek' >> /etc/environment
    source /etc/environment

#### Changing interface and network scope
    sudo nano $PREFIX/etc/node.cfg
    
    [zeek]  
    type=standalone  
    host=localhost  
    interface=eno1 *   
    
```
sudo nano $PREFIX/etc/networks.cfg
        
192.168.1.0/24  Local network
```

#### Add User To 'zeek' Group  
    sudo usermod -aG zeek $USER     # logout, log back in

<br>

## Start/Stop Zeek
#### Start
```
cd $PREFIX/bin && sudo ./zeekctl  
[ZeekControl] >  install  
[ZeekControl] >  start
```
#### Stop
```
[ZeekControl] > stop  
[ZeekControl] > exit
```

<br>

## Reviewing Logs
```
cd $PREFIX/logs/{date}    # 'current' if zeek is running  
sudo gzip -d {file.log.gz}
tail -n +7 {file.log} | cut -d $'\t' -f {column numbers}     # ex: tail -n +7 C98XEG~9.LOG | cut -d $'\t' -f 3-6 (row uid, source port, dest port)
```

- conn*.log: All connections seen within the monitored network scope. Fields include timestamp, source(orig) IP, destination(resp) IP, ports, services, protocols, bytes transmitted/recieved, etc.
- known_services*.log: Application and protocol services observed on then network by zeek
- weird*.log: Unusual activity (e.g. malformed packets, port-traffic mismatch, detected malfunctions)

#### Single record
    cat {file.log} | grep {uid of record}

<br>

## Formatting Logs with zeekcut
...

<br>

## Splunk Integration
...


