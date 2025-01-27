## How to make the docker integration with wsl permanently

**Step 1**: Add Docker Host Configuration to .zshrc
Since you're using Zsh, update your `~/.zshrc` instead of `~/.bashrc`:
```bash
echo 'export DOCKER_HOST=unix:///run/docker.sock' >> ~/.zshrc
```
Apply the changes:
```bash
source ~/.zshrc
```

**Step 2**: Ensure Docker Starts with WSL
To make sure Docker is always accessible in WSL2, follow these:

1. Enable WSL2 Integration in Docker Desktop

    * Open Docker Desktop → Settings → Resources → WSL Integration.
   * Enable integration for your WSL2 distro (Ubuntu).
   * Enable "Start Docker Desktop when you log in" in Settings → General.

2. Restart WSL to apply changes:
```bash
wsl --shutdown
```
3. Check Docker Availability
Reopen WSL and run:
```bash
docker --version
```


## How to create container in wsl for openwebui
```bash
docker run -d \
  --name openwebui-new \
  -p 3000:3000 \
  -v openwebui-data:/app/backend/data \
  -e OLLAMA_BASE_URL=http://172.20.76.151:11434 \
  ghcr.io/open-webui/open-webui:main
```

here use your own ip address and map ports

### If you want to delete existing container
```bash
docker rm -f openwebui
```



