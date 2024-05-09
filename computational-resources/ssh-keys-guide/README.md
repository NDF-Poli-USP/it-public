# Creating SSH Keys Guide

SSH keys are a safe way to log into machines remotely without providing your username and password.

⚠️ WARNING: your private key should be kept at a safe location in your computer at all times. Do not share it with anyone. If you lose your keys, contact NDF's support immediately.

## Linux

- Open the terminal
- Generate new keys
```
ssh-keygen -o -a 256 -t ed25519 -C "$(whoami)-$(hostname)-$(date +'%d-%m-%Y')"
```
- Continue with `Enter` on all fields
- Copy the contents of the public key
```
cat ~/.ssh/id_ed25519.pub
```

### To use the Linux keys

These steps will have to be taken on every login to your system

- Navigate to the folder containing the keys
```
cd ~/.ssh
```
- Start an ssh-agent
```
eval `ssh-agent -s`
```
- Add the keys to the agent
```
ssh-add id_ed25519
```
## Windows 10 and 11

- Open the command prompt (Search>**Command Prompt (do not use Power Shell)**>Right Click and Run as administrator)

![image](https://github.com/NDF-Poli-USP/it-public/assets/158466624/a585d9b0-1b92-4db7-b6ff-c0a4cf76628f)

- Create new keys

```
ssh-keygen -t ed25519 -C "%username%-%COMPUTERNAME%-%date:~0,2%-%date:~3,2%-%date:~6,4%"
```

- Continue with `Enter` on all fields
- Copy the contents of the public key to send it to the systems administrator
```
type %userprofile%\.ssh\id_ed25519.pub
```

![image](https://github.com/NDF-Poli-USP/it-public/assets/158466624/c9b0dbff-11b4-488d-8456-5bd0356398fb)

