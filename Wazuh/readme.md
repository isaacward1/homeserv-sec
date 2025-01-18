### [Documentation](https://documentation.wazuh.com/current/index.html)

## Install
    curl -sO https://packages.wazuh.com/4.9/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
    # Copy/save provided password


<br>

## Changing dashboard access port
    sudo vim /etc/wazuh-dashboard/opensearch_dashboards.yml
    
    # server.port: 8444 <--- change this
    
    sudo systemctl restart wazuh-dashboard

<br>

## Opening ports
    sudo ufw proto tcp allow from {client local IP} to any port 1514,1515,8444 comment 'wazuh'

<br>

## Changing default admin password
    curl -so wazuh-passwords-tool.sh https://packages.wazuh.com/4.9/wazuh-passwords-tool.sh
    bash wazuh-passwords-tool.sh -u admin -p {new password}
    sudo systemctl restart wazuh-dashboard filebeat
    echo "clear browser cache"

<br>

## Adding Agent
1. Navigate to https://{server IP}:8444/
2. 'Server Management' >> 'Endpoints Summary' >> 'Deploy New Agent'
3. Select OS (Windows), etc.
4. Copy (a):
    
        Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.10.0-1.msi -OutFile $env:tmp\wazuh-agent; msiexec.exe /i $env:tmp\wazuh-agent /q WAZUH_MANAGER='{Server IP}' WAZUH_AGENT_GROUP='default' WAZUH_AGENT_NAME='{Agent name}'

        NET START WazuhSvc

5. 
- Windows + R, "powershell.exe", Ctrl+Shift+Enter
- Paste (a) into PowerShell Terminal

<br>

## Applying Patches to [Vulnerable Machines](https://github.com/rapid7/metasploitable3)
...
    
