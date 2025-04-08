<h2 align=center>Gensyn Testnet Node Guide</h2>

## 💻 System Requirements

| Requirement                         | Details                                                     |
|-------------------------------------|-------------------------------------------------------------|
| **CPU Architecture**                | `arm64` or `amd64`                                          |
| **Recommended RAM**                 | 24 GB                                                       |
| **CUDA Devices (Recommended)**      | `RTX 3090`, `RTX 4070`, `RTX 4090`, `A100`, `H100`          |
| **Python Version**                  | Python >= 3.10 (For Mac, you may need to upgrade)           |


## 🌐 Rent GPU
- Visit : [Quick Pod Website](https://console.quickpod.io?affiliate=64e0d2b2-59ee-4989-a05f-f4c3b6dbb2e4)
- Sign Up using email address
- Go to your email and verify your Quick Pod account
- Click on `Add` button in the corner to deposit fund
- You can deposit using crypto currency (from metamask) or using Credit card
- Now go to `template` section and then select `Ubuntu 22.04 jammy` in the below
- Now click on `Select GPU` and search `RTX 4090` and choose it
- Now choose a GPU and click on `Create POD` button
- Your GPU server will be deployed soon
- You can simply click on `Connect` button and then choose `Connect to Web Terminal`
- But if you are using different gpu/vps provider then you should use `Connect via SSH` method mentioned below

## 🛜 Connect via SSH

- First open a terminal (this could be either WSL / Codespace / Command Prompt)
- Use this below command to generate SSH-Key
```
ssh-keygen
```
- It will ask 3 questions like this :
```
Enter file in which to save the key (/home/codespace/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again: 
```
- You need to press `Enter` 3 times
- After that you will get a message like this on your terminal
```
Your public key has been saved in /home/codespace/.ssh/id_rsa.pub
```
- `/home/codespace/.ssh/id_rsa.pub` is the path of this public key in my case, in your case it might be different

![Screenshot 2025-04-08 081948](https://github.com/user-attachments/assets/035803da-c5bb-454e-9db4-4459e2123128)

- You should use this command to see those ssh key :
    - If you are using Linux/macOS (WSL) : `cat path/of/that/publickey` , in my case, it would be : `cat /home/codespace/.ssh/id_rsa.pub`
    - If you are using Command Prompt : `type path\of\that\publickey`, in my case, it would be : `type \home\codespace\.ssh\id_rsa.pub`
    - If you are using PowerShell : `Get-Content path\of\that\publickey`, in my case, it would be : `Get-Content \home\codespace\.ssh\id_rsa.pub`
- Now copy this public key and go to hosting provider from where you bought GPU
- After visiting the web hosting provider website, navigate to settings and there paste and save your ssh key
- Now, copy the command you received after renting the GPU instance and paste it into the terminal where you generated the public key.
- In my case, the command looks like this:
```
ssh -p 69 root@69.69.69.69
```
- Now paste this command on this terminal to access your GPU server

## 📥 Installation

1. **Install `sudo`**
```bash
apt update && apt install -y sudo
```
2. **Install other dependencies**
```bash
sudo apt update && sudo apt install -y python3 python3-venv python3-pip curl wget screen git lsof nano unzip
```
3. **Install Node.js and npm**  
```bash
curl -sSL https://raw.githubusercontent.com/zunxbt/installation/main/node.sh | bash
```
4. **Clone this repository**
```bash
cd $HOME && [ -d rl-swarm ] && rm -rf rl-swarm; git clone https://github.com/zunxbt/rl-swarm.git && cd rl-swarm
```
5. **Create a `screen` session**
```bash
screen -S gensyn
```
6. **Run the swarm**
```bash
python3 -m venv .venv && . .venv/bin/activate && ./run_rl_swarm.sh
```
- It will ask some questions, you should send response properly
- ```Would you like to push models you train in the RL swarm to the Hugging Face Hub? [y/N]``` : Write `N`
- When you will see interface like this, you can detach from this screen session

![Screenshot 2025-04-01 061641](https://github.com/user-attachments/assets/b5ed9645-16a2-4911-8a73-97e21fdde274)

7. **Detach from `screen session`**
- Use `Ctrl + A` and then press `D` to detach from this screen session.

 ## 🔄️ Back up `swarm.pem`
After running the Gensyn node, it is essential to back up the swarm.pem file from your remote server (GPU or VPS) to your local PC. If you lose this file, your contribution will also be lost. Some GPU servers do not support SCP or SFTP, so I will provide distinct methods — one specifically for GPU servers and another for VPS.

### 1. Back up `swarm.pem` from GPU server to local PC
- For this, you must need to connect to GPU server using [SSH](https://github.com/zunxbt/gensyn-testnet?tab=readme-ov-file#-connect-via-ssh) (Recommened to do these stuffs on Command Prompt or Power Shell)
- Now exit from this GPU server using this command
```
exit
```
- Now replace `SSH-COMMAND` in the below command with the command which your received from provider, then replace `YOUR-PC-PATH` where you want to download this swarm.pem file and then execute it on your Command prompt or Power shell
```
SSH-COMMAND "cat ~/rl-swarm/swarm.pem" > "YOUR-PC-PATH\swarm.pem"
```
- In my case, this command looks like this :
```
ssh -p 69 root@69.69.69.69 "cat ~/rl-swarm/swarm.pem" > "C:\Users\USER\Downloads\swarm.pem"
```
- Done, your `swarm.pem` file is now saved on your local system

### 2. Back up `swarm.pem` from VPS server to local PC
- For this, I recommend to use `Command Prompt` or `Power Shell`
- If you are using **Command Prompt** then use the below commmand, make sure to replace `VPS-USERNAME` , `VPS-IP`and `YOUR-PC-PATH` (where you want to save swarm.pem file) with actual value
```
scp VPS-USERNAME@VPS-IP:~/rl-swarm/swarm.pem "YOUR-PC-PATH"
```
- In my case this command looks like this :
```
scp root@69.69.69.69:~/rl-swarm/swarm.pem "C:\Users\USER\Downloads"
```
- If you are using **Powershell** then use the below commmand, make sure to replace `VPS-USERNAME` , `VPS-IP`and `YOUR-PC-PATH`(where you want to save swarm.pem file) with actual value
```
scp VPS-USERNAME@VPS-IP:~/rl-swarm/swarm.pem 'YOUR-PC-PATH'
```
- In my case this command looks like this :
```
scp root@69.69.69.69:~/rl-swarm/swarm.pem 'C:\Users\USER\Downloads'
```

### 3. Back up `swarm.pem` from WSL to local PC
- First, open `Command Prompt` or `Windows Powershell`
- Then use the below command, make sure to replace `YOUR-WSL-USERNAME` `YOUR-PC-PATH`(where you want to save swarm.pem file) with actual value
```
copy "\\wsl$\Ubuntu\home\YOUR-WSL-USERNAME\rl-swarm\swarm.pem" "YOUR-PC-PATH"
```
- In my case, it looks like this
```
copy "\\wsl$\Ubuntu\home\zun24\rl-swarm\swarm.pem" "C:\Users\USER\Downloads"
```

## 🟢 Node Status

### 1. Check Logs
- To check whether your node is running or not, you can check logs
- To check logs you need to re-attach with screen session, so use the below command
```
screen -r gensyn
```
- If you see everything running then it's fine
- Now detach from this screen session, Use `Ctrl + A` and then press `D` to detach from this screen session.
- Everytime you reattach, every time you should detach

### 2. Check Wins
- Visit : https://gensyn-node.vercel.app/
- Enter Peer-ID that you often see this in your logs
- The more win, the better

**If you see `0x0000000000000000000000000000000000000000` in `Connected EOA Address` section, that means your contribution is not being recorded, so you should run the node from beginning with fresh new email**
