### [Documentation](https://documentation.wazuh.com/current/index.html)

## Install
    curl -sO https://packages.wazuh.com/4.9/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
- Copy/save provided password
- https://{server IP}:8444/

<br>

## Dashboard
### Changing dashboard access port
    sudo vim /etc/wazuh-dashboard/opensearch_dashboards.yml
    
    # server.port: 8444 <--- change this

    ufw allow from {server IP}/24 to any port 8444 comment 'wazuh dash local access'
    sudo systemctl restart wazuh-dashboard

### Adding Agents
1. Server Management >> Endpoints Summary >> Deploy New Agent
2. Copy (a):
    
       Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.9.2-1.msi -OutFile $env:tmp\wazuh-agent; msiexec.exe /i $env:tmp\wazuh-agent /q WAZUH_MANAGER='{server IP}' WAZUH_AGENT_NAME='Windows_Dummy'

       NET START WazuhSvc

4. On Windows Client:
- Windows + R, "powershell.exe", Ctrl+Shift+Enter
- Paste (a) into PowerShell Terminal

<br>

## Changing default admin password
    curl -so wazuh-passwords-tool.sh https://packages.wazuh.com/4.9/wazuh-passwords-tool.sh
    bash wazuh-passwords-tool.sh -u admin -p {new password}
    sudo systemctl restart wazuh-dashboard filebeat
    echo "clear browser cache"
