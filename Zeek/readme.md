## Install

    echo 'deb http://download.opensuse.org/repositories/security:/zeek/xUbuntu_24.04/ /' | sudo tee /etc/apt/sources.list.d/security:zeek.list
    curl -fsSL https://download.opensuse.org/repositories/security:zeek/xUbuntu_24.04/Release.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/security_zeek.gpg > /dev/null
    sudo apt update
    sudo apt install zeek
    # No postfix configuration

# Setup

    sudo echo zeekdir='/opt/zeek' >> /etc/environment
    source /etc/environment
    sudo nano $zeekdir/etc/node.cfg
        [zeek]
        type=standalone
        host=localhost
        interface=eno1

    

    
    
