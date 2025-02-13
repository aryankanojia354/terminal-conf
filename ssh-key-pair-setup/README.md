# Setting up SSH Key Pair for GitHub on WSL2

## 1. Generate SSH Key Pair
Open your WSL2 terminal and run the following command:

```bash
ssh-keygen -t rsa -b 4096 -C "aryankanojia354@gmail.com"
```

## 2. Add SSH Key to SSH Agent
Start the SSH agent:
Then, add your SSH private key:
Display your public SSH key:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub
```
## 3. Test Connections
```bash
ssh -T git@github.com
```
## 4. Now go in Github and paste the key

## 5. Now all set!
![alt text](image.png)

