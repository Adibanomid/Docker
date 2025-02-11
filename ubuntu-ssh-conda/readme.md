# make sure the miniconda.sh package file is downloaded in the packages directory (due to it's huge size it can't be uploaded on GitHub repo)

# builld image
docker buildx build . -t <image-name>:latest
docker buildx build . -t omidimage:latest

# run image
docker run -itd --name <container-name> -p 2222:22 -p 8001:8000 <image-name>
docker run -itd --name testomid -p 2222:22 -p 8001:8000 omidimage

# enter container
docker exec -it <container-name> bash
docker exec -it testomid bash



# ssh access to container
ssh-keygen -R <container-internal-port> -y
ssh-keygen -R 172.17.0.3 -y

ssh <username>@<container-internal-port>
ssh superdeveloper@172.17.0.3

# docker compose build
docker compose -f docker-compose.yaml -p testcompose up -d



