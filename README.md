## Server Service
default service for control and config server

### RUN
`cd /projects/`
`sudo docker compose -f docker-compose.services.yml -p service up -d`

**if you don't Accesses Sudo**

`newgrp docker`
`docker compose -f docker-compose.services.yml -p service up -d`

### Down Service
`cd /projects/`
`sudo docker compose -f docker-compose.services.yml -p service down`

