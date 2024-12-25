## Install
1. Download Nessus essentials .deb package

        curl --request GET \
        --url 'https://www.tenable.com/downloads/api/v2/pages/nessus/files/Nessus-10.8.3-ubuntu1604_amd64.deb' \
        --output 'Nessus-10.8.3-ubuntu1604_amd64.deb'

3. Install, start service

        sudo dpkg -i <Nessus package.deb>
        sudo systemctl start nessusd

5. Navigate to https://<server ip>:8843

6. Select Nessus Essentials Trial, Enter Activation Key

7. Wait 7 hours for plugins to install

## Create Scan
...
