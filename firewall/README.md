# Firewall Configuration – UFW on web server

This project configures a basic firewall using UFW (Uncomplicated Firewall) on the web server to enhance security by restricting incoming traffic.

##  Requirements

- Block all incoming traffic by default.
- Allow only the following TCP ports:
  - **22** – SSH (remote access)
  - **80** – HTTP (web traffic)
  - **443** – HTTPS (secure web traffic)

##  Commands Used

```bash in your server
sudo apt update
sudo apt install ufw -y
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
