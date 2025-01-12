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
1. Change zeek .log formatting to JSON (default = tsv)

       sudo vim /opt/zeek/share/zeek/site/local.zeek

       @load policy/tuning/json-logs <-- append this to the bottom

2. On splunk dashboard: Settings >> Forwarding and Recieving >> Receive data >> (+) Add New >> Listen on this port: 9997 >> Save
3. Allow through firewall:

        sudo ufw allow proto tcp from {local IP subnet} to any port 9997 comment 'splunk reciever 1'

4. Add 'TA for Zeek' (A Splunk Add-on for Zeek): Apps >> Find More Apps >> search: 'TA for Zeek' >> Install
5. 

<br>

## Suricata Inegration
...

