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


Add User To 'Zeek' Group

> sudo usermod -aG zeek $USER  
> ogout, log back in

<br>

## Start Zeek

> cd $PREFIX/bin && sudo ./zeekctl  
[ZeekControl] >  install  
[ZeekControl] >  start

## Stop Zeek
> [ZeekControl] > stop  
> [ZeekControl] > exit

## Reviewing Logs
> cd $PREFIX/logs/{date}
> sudo gzip -d {file.log.gz}
> cat {file.log}
    

    
    
