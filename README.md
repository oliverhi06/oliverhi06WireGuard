# 
From the console on your shiny new VM, you need to install docker using the slew of commands graciously provided to you by the official docker documentation
```bash
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
```
After that, you can install docker
```console
 sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Now we need to install wireguard for docker.
The website that you provided in the powerpoint was down when I did this project, so I used [this guy's](https://youtu.be/c2vOleGvJ_Y?si=qGxQ0ifQ53YfkRsN) tutorial on youtube. 
He says to do all this in the /opt directory in root, so go there and make a wireguard directory

`cd /opt`
`mkdir wireguard`
`cd wireguard`

Then, make a new .yaml file and paste the sample file from [here](https://github.com/linuxserver/docker-wireguard)
`nano docker-compose.yaml`
`{Paste}`

You will need to change two environment variables:
	SERVERURL: replace this with your machine's IP
	PEERS: replace this with the number of that will be using the VPN. In my case, 2
And, in the volumes field, change the wireguard config directory to wherever the installation is. Here, it's in /opt/wireguard/config

Otherwise, we're good to go. Exit nano and use
`docker compose up -d`
If everything works as intended, wireguard should be up and running, (you can check with `docker ps`) and it should have created 2 config files. I used filezilla to scp both of these out. 

On my iPhone I just had to download the wireguard and scan the QR code that was in the config folder. On my PC, you just have to download the wireguard client from [here](https://www.wireguard.com/install/)and import the .conf file that was scp'd out. Other than that, it should just work!
Here are the screenshots that show my changed IP:
Before:
<img width="1272" height="774" alt="Pasted image 20251124112520" src="https://github.com/user-attachments/assets/0d64b92f-a439-4f2c-8808-ca4133ae7528" />
<img width="590" height="1278" alt="Untitled 1" src="https://github.com/user-attachments/assets/1000629a-4eb8-40b3-9674-82ff6abeb1c3" />

After: 
<img width="1269" height="817" alt="Pasted image 20251124112739" src="https://github.com/user-attachments/assets/90a4a99c-3751-4854-83ca-bd2b0d4e35ce" />
<img width="590" height="1278" alt="Untitled-1" src="https://github.com/user-attachments/assets/2f5c506e-5f4e-4941-a2ca-bd4321b3eb12" />

