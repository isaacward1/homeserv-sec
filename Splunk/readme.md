## Setup
#### Add User to 'splunk' group
    sudo usermod -aG splunk $USER  # logout/in

#### Permissions
    sudo chown -R splunk:splunk /opt/splunk/var

#### Change splunk mgmt IP
    # in splunk-launch.conf
        * SPLUNK_BINDIP=0.0.0.0
    
    # in web.conf
        * mgmtHostPort=0.0.0.0:8089
    
    sudo ./splunk restart

#### Fix 'Bad regex value: '([\r\n+)', of param: props.conf / [Zeek_conn_log]...' error
    sudo nano /opt/splunk/etc/apps/search/local/props.conf

    [Zeek_conn_log]
    DATETIME_CONFIG = 
    LINE_BREAKER = ([\r\n+) <-- append ']'
    NO_BINARY_CHECK = true
    category = Custom
    pulldown_type = true


    

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

       @load policy/tuning/json-logs.zeek <-- append this to the bottom

2. Refresh zeek config

       sudo /opt/zeek/bin/zeekctl install

4. Splunk Dashboard Settings >> Forwarding and Recieving >> Receive data >> (+) Add New >> Listen on this port: 9997 >> Save
5. Allow through firewall:

        sudo ufw allow proto tcp from {local IP subnet} to any port 9997 comment 'splunk reciever 1'

6. Add 'TA for Zeek' (A Splunk Add-on for Zeek): Splunk Dashboard Apps >> Find More Apps >> search: 'TA for Zeek' >> Install
7. Splunk Dashboard Settings >> Indexes >> New Index >> Index name: 'Zeek' >> Save

8. [Download Splunk Forwarder](https://www.splunk.com/en_us/download/universal-forwarder.html)

       sudo dpkg -i {splunkforwarder.deb}
        
9. Configure forwarding rules

    sudo vim /etc/splunkforwarder/etc/system/local/inputs.conf
       
10. Add Forwarder:

       cd /opt/splunk/bin && ./splunk add forward-server {server IP}:9997

       nano /opt/splunkforwarder/etc/system/local/inputs.conf
   
       [default]
       host = {server hostname}
    
       [monitor:///opt/zeek/logs/current]
       _TCP_ROUTING = *
       index = zeek
       sourcetype = bro:json

11. Start forwarder

    cd /opt/splunkforwarder/bin && ./splunk start

12. 

<br>

## Suricata Inegration
...

