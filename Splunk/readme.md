## Setup
#### Add User to 'splunk' group
    sudo usermod -aG splunk $USER  # logout/in

#### Change splunk mgmt IP
    # in splunk-launch.conf
        * SPLUNK_BINDIP=0.0.0.0
    
    # in web.conf
        * mgmtHostPort=0.0.0.0:8089
    
    sudo ./splunk restart

#### Allow local access to splunk dashboard
    sudo ufw allow from 192.168.1.0/24 to any port 8000 comment 'splunk local access'

<br>

## Start/Stop Splunk
#### Start
    cd /opt/splunk/bin && ./splunk start 
#### Stop
    cd /opt/splunk/bin && ./splunk stop

<br>

## Zeek Integration
...

<br>

## Suricata Inegration
...

