# Unevenr-Wireguard-Installation-Guide

Guides followed: https://thematrix.dev/install-docker-and-docker-compose-on-ubuntu-20-04/

Made a Digitial Ocean account
    created a project with docker 

**In the console (while also following guide):**

Installs tools:
    sudo apt install apt-transport-https ca-certificates curl software-properties-common -y

Creates Docker key
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Add Docker repo:
    sudo add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) \
    stable"

Switch to correct repo:
    apt-cache policy docker-ce

Install Docker:
    sudo apt install docker-ce -y

Installs Docker compose
    sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

Sets permissions:   
    sudo chmod +x /usr/local/bin/docker-compose

Make nessesary files:
    mkdir -p ~/wireguard/
    mkdir -p ~/wireguard/config/
Nano into it:
    nano ~/wireguard/docker-compose.yml

Copy and paste the following:
        version: '3.8'
    services:
    wireguard:
        container_name: wireguard
        image: linuxserver/wireguard
        environment:
        - PUID=1000
        - PGID=1000
        - TZ=America/Chicago
        - SERVERURL=1146.190.51.105
        - SERVERPORT=51820
        - PEERS=3
        - PEERDNS=auto
        - INTERNAL_SUBNET=10.0.0.0
        ports:
        - 51820:51820/udp
        volumes:
        - type: bind
            source: ./config/
            target: /config/
        - type: bind
            source: /lib/modules
            target: /lib/modules
        restart: always
        cap_add:
        - NET_ADMIN
        - SYS_MODULE
        sysctls:
        - net.ipv4.conf.all.src_valid_mark=1

Goes into Wireguard and runs it:
    cd ~/wireguard/
    docker-compose up -d

Allows you to connect Wireguard to your phone:
    docker-compose logs -f wireguard

Downloaded app on my phone

Scanned QR code

Took screenshots:

    Mobile:
        With VPN off:
![Phone VPN OFF](https://github.com/Unevenr/Unevenr-Wireguard-Installation-Guide/assets/112726183/85f62a46-6f61-462d-9abc-e2bff243dd22)

        With VPN on:
![Phone VPN ON](https://github.com/Unevenr/Unevenr-Wireguard-Installation-Guide/assets/112726183/aafecbf8-d6d5-4ca8-a2b9-82c87f3a5838)
![Phone VPN ON2](https://github.com/Unevenr/Unevenr-Wireguard-Installation-Guide/assets/112726183/885fb7be-6adb-49b7-83e8-cd10968bae34)

    PC:
<img width="959" alt="Wireguard PC Test" src="https://github.com/Unevenr/Unevenr-Wireguard-Installation-Guide/assets/112726183/98148d3e-173f-4bdf-97ce-3bee175f3d8a">


    
