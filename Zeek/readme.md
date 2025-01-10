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
    
> sudo nano $PREFIX/etc/node.cfg

[zeek]  
type=standalone  
host=localhost  
interface=eno1

> sudo nano $PREFIX/etc/networks.cfg

192.168.1.0/24  Local network

<br>

## Add User To 'zeek' Group

> sudo usermod -aG zeek $USER  
> ogout, log back in

<br>

## Start Zeek
> cd $PREFIX/bin && sudo ./zeekctl  
[ZeekControl] >  install  
[ZeekControl] >  start

<br>

## Stop Zeek
> [ZeekControl] > stop  
> [ZeekControl] > exit

<br>

## Reviewing Logs
> cd $PREFIX/logs/{date}  <-- 'current' if zeek is running  
> sudo gzip -d {file.log.gz}  
> cat {file.log}

conn*.log = All connections seen within the monitored network scope. Fields include timestamp, source(orig) IP, destination(resp) IP, ports, services, protocols
"Contains an entry for every connection seen on the wire, with basic properties such as time and duration, originator and responder IP addresses, services and ports, payload size, and much more. This log provides a comprehensive record of the network’s activity."
