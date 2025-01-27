# OpenWebUI Setup for Ollama Models in WSL2

## Step 1: Run OpenWebUI with Docker

Use the following command to set up OpenWebUI with Docker:

```sh
docker run -d \                                                                 
  --name openwebui \
  -p 3000:8080 \
  -v openwebui-data:/app/backend/data \
  -e OLLAMA_BASE_URL=http://<your-ip>:11434 \
  ghcr.io/open-webui/open-webui:main
```

Replace `<your-ip>` with your actual IP address. To find your IP address, use:

```sh
ip addr show eth0 | grep 'inet\b' | awk '{print $2}' | cut -d/ -f1
```

## Step 2: Start OpenWebUI

Once the container is set up, start OpenWebUI using:

```sh
docker start openwebui
```

## Step 3: Configure Ollama to Serve on All IP Addresses

By default, Ollama is configured to serve only on localhost. Since WSL2 and Docker run on different networks, you need to allow Ollama to serve for all IP addresses.

Edit the Ollama service configuration file and add the following line:

```
sudo systemctl edit --full ollama
Environment="OLLAMA_HOST=0.0.0.0:11434"
```

### Updated `ollama.service` File:

```
[Unit]
Description=Ollama Service
After=network-online.target

[Service]
ExecStart=/usr/local/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3
# Add the OLLAMA_HOST variable here ▼
Environment="OLLAMA_HOST=0.0.0.0:11434"
Environment="PATH=/home/aryan/.nvm/versions/node/v22.13.0/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"

[Install]
WantedBy=default.target
```

## Step 4: Restart Ollama Service

After updating the configuration, restart the Ollama service to apply changes:

```sh
sudo systemctl daemon-reload
sudo systemctl restart ollama
```

## Step 5: Verify Setup

Check if OpenWebUI is running by accessing `http://localhost:3000` in your browser.

If models are still not visible, ensure Ollama is correctly serving on all interfaces:

```sh
curl http://<your-ip>:11434/api/tags
```

This should return a list of available models.

