<h2 align=center>Gensyn Testnet Node Guide</h2>

## 💻 System Requirements

| Requirement                        | Details                                                                                      |
|-------------------------------------|---------------------------------------------------------------------------------------------|
| **CPU Architecture**                | `arm64` or `amd64`                                                                            |
| **Minimum RAM**                     | 16 GB                                                                                       |
| **CUDA Devices (optional)**         | `RTX 3090`, `RTX 4090`, `A100`, `H100`                                                  |
| **Python Version**                  | Python >= 3.10 (For Mac, you may need to upgrade) 

## 📥 Installation

https://github.com/user-attachments/assets/58fbad1f-11c4-40d6-a176-75b32bc19636

1. **Install Node.js and npm if not installed already**  
```bash
curl -sSL https://raw.githubusercontent.com/zunxbt/installation/main/node.sh | bash
```
2. **Install other dependencies**
```bash
sudo apt update && sudo apt install -y python3 python3-venv python3-pip curl screen git yarn && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && sudo apt update && sudo apt install -y yarn
```
3. **Clone this repository**
```bash
rm -rf rl-swarm && git clone https://github.com/zunxbt/rl-swarm.git && cd rl-swarm
```
4. **Create a `screen` session**
```bash
screen -S gensyn
```
5. **Run the swarm**
```bash
python3 -m venv .venv && source .venv/bin/activate && ./run_rl_swarm.sh
```

- It will show like this :
  
![image](https://github.com/user-attachments/assets/71072384-be3e-4515-a4c7-752b6a7c51c4)

You need to visit the URL which you will find on your terminal there and then, log in using your email. After logging in, it will display something like this

![Screenshot 2025-04-01 060920](https://github.com/user-attachments/assets/8ae77402-350e-4cd4-9f59-b1f37f92016b)

- It will ask you this question : `Would you like to push models you train in the RL swarm to the Hugging Face Hub? [y/N]` ; You should write `N` there
- You will see something like this; it indicates that everything is working fine. You can now detach from this screen session.
![Screenshot 2025-04-01 061641](https://github.com/user-attachments/assets/73a3f1ce-d824-4bdc-8df6-5c629a79cffc)

6. **Detach from `screen session`**
- Use `Ctrl + A` and then press `D` to detach from this screen session.

## ⚠️ OTP Issue / URL not accessible :
- If you can't get OTP in your email and also can't login using google, then use this method :
- Install ngrok in different tab on the same vps ( don't close previous tab where gensyn is running)

- For x86 ( amd64) Servers ; 

```bash
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz && tar -xvzf ngrok-v3-stable-linux-amd64.tgz && sudo mv ngrok /usr/local/bin/
```

- For aarch64 (arm64 ) Servers ; 

```bash
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-arm.tgz && tar -xvzf ngrok-v3-stable-linux-arm.tgz && sudo mv ngrok /usr/local/bin/
```

- Now visit : https://ngrok.com/
- Sign up using email
- Now go to `Your authtoken` section and then click on "show authtoken" option and then copy that command
- Now open your VPS in other tab and paste the command
- Now use this command `ngrok http 3000`
- Then click on the following url with ngrok domain and then access gynsyn page and login using email address (✅ working, tested)
