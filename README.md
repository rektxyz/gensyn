# 💻 Gensyn-ai-Rl-Swarm Guide (Mac/Linux/VPS) 💻

## 🖥️ Device/System Requirements

<img width="602" height="387" alt="image" src="https://github.com/user-attachments/assets/f52876c3-7bd7-4f1f-859a-ab381c2373da" />


---

## 🔑 Open Your VPS

```bash
ssh username@ip
```

---

# ⚙️ Pre-Requirements

## Install Python and Other Tools

### For Linux/WSL

```bash
sudo apt update && sudo apt install -y python3 python3-venv python3-pip curl wget screen git lsof
```

### For Mac

```bash
brew install python
```

### Check Python Version

```bash
python3 --version
```

---

## Install Node.js, npm & yarn

### Linux/WSL

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt update && sudo apt install -y nodejs
```

### Install Yarn (Linux)

```bash
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/s2.list > /dev/null
sudo apt update && sudo apt install -y yarn
```

### For Mac

```bash
brew install node
corepack enable
npm install -g yarn
```

### Check versions

```bash
node -v
npm -v
yarn -v
```

---

# 👨🏻‍💻 Start the Node (Linux/Mac)

## 1️⃣ Create a screen session (VPS only)

```bash
screen -S gensyn
```

## 2️⃣ Clone RL-Swarm Repo

```bash
git clone https://github.com/gensyn-ai/rl-swarm.git
```

## 3️⃣ Navigate to rl-swarm

```bash
cd rl-swarm
```

## 4️⃣ Create & Activate Virtual Environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

## 5️⃣ Run the swarm Node

```bash
./run_rl_swarm.sh
```

Follow login instructions.

### ⚠️ Important Prompts:

* "Push models to HF Hub?" → **N**
* "Enter model name" → **Press Enter (Default recommended)**
* "Participate in AI Prediction Market?" → **Y**

---

## 5️⃣ Choose Custom Models (Optional — Recommended for Mac)

* Gensyn/Qwen2.5-0.5B-Instruct
* Qwen/Qwen3-0.6B
* nvidia/AceInstruct-1.5B
* dnotitia/Smoothie-Qwen3-1.7B
* Gensyn/Qwen2.5-1.5B-Instruct

---

# 🔌 Detach & Attach from screen

* **Detach:** `Ctrl + A + D`
* **Attach:** `screen -r gensyn`

---

# 🛠 FAQ & Troubleshooting

## 1️⃣ How to access `http://localhost:3000` in VPS?

### Allow firewall ports

```bash
sudo apt install ufw -y
sudo ufw allow 22
sudo ufw allow 3000/tcp
sudo ufw enable
```

### Install cloudflared

```bash
wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
sudo dpkg -i cloudflared-linux-amd64.deb
cloudflared --version
```

### Run tunnel

```bash
cloudflared tunnel --url http://localhost:3000
```

Open the generated link in your local browser.

---

## 2️⃣ How to get the Node Name?

(Images can be added)

---

## 3️⃣ Save your swarm.pem file

### Copy swarm.pem to your local machine

```bash
scp USERNAME@YOUR_IP:~/rl-swarm/swarm.pem ~/swarm.pem
```

---

## 4️⃣ How to start next day?

```bash
cd rl-swarm
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

---

## 6️⃣ Resolve Terminated Error

```bash
deactivate
rm -rf .venv
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

If still terminated → restart or wait a few minutes.

---

# 🐝 SWARM Role & Telegram Bot Setup

## 1. Install Go

### Linux/WSL

```bash
cd ~
wget https://go.dev/dl/go1.24.0.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.24.0.linux-amd64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
echo 'export GOPATH=$HOME/go' >> ~/.bashrc
echo 'export PATH=$PATH:$GOPATH/bin' >> ~/.bashrc
source ~/.bashrc
```

Check:

```bash
go version
```

### Mac

```bash
brew install go
```

---

## 2. Telegram Bot Setup 🤖

### 2.1 Create bot

Go to **BotFather** → `/newbot` → Get token

### 2.2 Get Chat ID

Send a message to your bot, then visit:

```
https://api.telegram.org/botYOUR_BOT_TOKEN/getUpdates
```

---

# 3. Install & Configure GSwarm

```bash
go install github.com/Deep-Commit/gswarm/cmd/gswarm@latest
gswarm --version
gswarm
```

Enter:

* BotToken
* ChatID
* EOA address (from Gensyn dashboard)

---

# 4. Linking Discord & Telegram

* Go to Discord → `#swarm-link`
* Run `/link-telegram`
* Get code
* Send to Telegram bot:

```
/verify CODE
```

---


# 📈 Upgrade to New Release (CodeZero)

Follow these steps carefully to upgrade your Gensyn Swarm Node to the latest version.

### 🔄 1. Go to the Gensyn Screen (VPS)

```bash
screen -r gensyn
```

Return to your active Gensyn session.

### 🛑 2. Stop Your Node

```bash
ctrl + c
```

Stops the currently running node.

### 📁 3. Move to the RL-Swarm Directory

```bash
cd rl-swarm
```

### 🔌 4. Deactivate Current Environment

```bash
deactivate
rm -rf .venv
```

### ⬇️ 5. Pull the Latest Release

```bash
git switch main
git reset --hard
git clean -fd
git pull origin main
```

Cleans your repo and fetches the new update.

### 🚀 6. Start the Updated Swarm Node

```bash
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

Your node is now updated and running successfully! 🌟


<h3 align="center">Successful node looks like this ✅</h3>

<img width="1095" height="954" alt="image" src="https://github.com/user-attachments/assets/35e6b464-eca8-47d0-9a6b-3c8a32573351" />
