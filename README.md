# RL-Swarm Setup Guide

This guide walks you through setting up the `rl-swarm` project from scratch, including restoring a saved key, activating a virtual environment, running the service, and exposing it via a tunnel.

---

#### **System Requirements & Setup**

Before starting, make sure your system is updated and has all required dependencies installed:

### System Update & Essentials
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl wget git unzip build-essential python3-pip python3-venv nodejs screen nano
```

### Cloudflared Installation
```bash
wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64
chmod +x cloudflared-linux-amd64
sudo mv cloudflared-linux-amd64 /usr/local/bin/cloudflared
cloudflared --version
```

## **Steps**

### 1. Backup `swarm.pem` (if existing user)
Copy your key file to a safe location:
```bash
cp $HOME/rl-swarm/swarm.pem $HOME/
````

### 2. Clean and Clone Fresh Repo
Remove the old project and clone the fresh version:
```bash
cd $HOME && \
rm -rf rl-swarm && \
git clone https://github.com/kai25x/gensyn.git
```

### 3. Restore `swarm.pem`
Move the key file back into the cloned repo:
```bash
if you want to put your old swarm.pem then access your root folder then find rl-swarm folder after that put swarm.pem into it
```
```bash
cp $HOME/swarm.pem $HOME/rl-swarm/
```

### 4. Navigate and Start Screen Session
```bash
cd $HOME/rl-swarm
screen -S gensyn
```

### 5. Set Up Python Environment
Inside the `screen` session:
```bash
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

Wait for the message:
```
Waiting for localhost:3000...
```

Then **detach** the screen session:
```bash
Ctrl + A, then press D
```

---

## **Expose Localhost Port (3000)**

### Using Cloudflare Tunnel (Cloudflared)
```bash
sudo apt install cloudflared  # or brew install cloudflared on macOS
cloudflared tunnel --url http://localhost:3000
```

Open the given URL in your browser and log in.

---

## **Restore Screen Session**
To return to your background screen session:
```bash
screen -r gensyn
```

---

**Done!** You’re now back in your `gensyn` screen and ready to interact with the running service.
