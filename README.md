# n8n
Docker base n8n on a VPS Server with VOLUME to never loose your DATA.


✅ Step-by-step: Persistent n8n with Docker
1. Create a Docker Volume (optional but recommended)
```
 docker volume create n8n_data
```

   
## create files:

1. .env

2. docker-compose.yml


```
docker-compose up -d
```


________________________


Updating n8n in Docker is simple and safe — especially if you're using volumes for persistent data (like you are). Here's the safe and correct way to update:

```
docker run --rm -v n8n_data:/data -v $(pwd):/backup alpine \
  tar czf /backup/n8n-backup.tar.gz -C /data .
```
 
 ### Pull the latest n8n Docker image - Update to the latest version
```
docker pull n8nio/n8n:latest
```


### If you're using docker-compose:
```
docker compose down
```

### Start it again (with the updated image)
```
docker compose up -d
```

_____________________

## Manual Run latest version
docker run -d --name n8n \
  -v n8n_data:/home/node/.n8n \
  -p 5678:5678 \
  --env-file .env \
  n8nio/n8n:latest

_____________________


## Optional: Pin a specific version
If you want to avoid surprises from :latest, specify a version:

```
image: n8nio/n8n:1.45.0
```
You can check available tags here:
👉 https://hub.docker.com/r/n8nio/n8n/tags
