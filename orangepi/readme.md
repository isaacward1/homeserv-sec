### Burning image to micro ssd
1. install [Balena Etcher](https://etcher.balena.io/)
2. download preferred OS image/ISO: [Armbian - Debian 13 Minimal](https://dl.armbian.com/orangepi3b/Trixie_vendor_minimal)





<br>

### why tf does this use netplan??

sudo apt update && sudo apt upgrade -y


### yiiipppeeeeeee!
    sudo apt install ufw


#### fix ufw/iptables/nf_tables compatibility:

    sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
