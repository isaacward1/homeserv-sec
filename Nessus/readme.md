## Install
1. Download Nessus essentials .deb package

        curl --request GET \
        --url 'https://www.tenable.com/downloads/api/v2/pages/nessus/files/Nessus-10.8.3-ubuntu1604_amd64.deb' \
        --output 'Nessus-10.8.3-ubuntu1604_amd64.deb'

3. Install, start service

        sudo dpkg -i <Nessus package.deb>
        sudo systemctl start nessusd

5. Navigate to https://{server ip}:8843

6. Select Nessus Essentials Trial, enter activation key

7. Wait 7 hours for plugins to install

## SMTP Server
        
- Host: smtp.google.com
- Port: 587
- From (sender email): {email}@gmail.com
- Encryption: Force TLS
- Hostname: localhost:8834
- Auth Method: LOGIN


## Recurring Network Scan

1. '(+) New Scan'

2. 'Basic Network Scan'


- Name: Weekly Net Scan  
- Targets: {local IP range}  
- Schedule: Enabled  
          Freq: Weekly, Every Monday @ 4:00 AM EST  
- Notifications: {email}@gmail.com  
- Discovery: Port Scan (all ports)  
- Scan Type: Default           

        
