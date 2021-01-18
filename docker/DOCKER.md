# DOCKER:

## Adding user to docker group:

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```

## Running and changing containers:

```bash
docker pull \<images-name>:\<version> : pulls image from Docker registry
docker run \<images-name>:\<version> : runs container from mentioned image
docker ps : shows all running containers
docker ps -a: shows all available containers
docker exec: executes a command in a running container

# Run bash in python container
docker run -it python:3.5 bash
docker exec -it <container name/id> bash

# Create new image from running container after changes
docker commit -m "message" <container name/id> <new name>:<version>
docker commit -m "added date script" keen_aryabhata date_script:1.0

# Push image to dockerhub
docker login
docker tag <image_name> <your_docker_hub_username>/<image>:<version>
docker push <your_docker_hub_username>/<image>:<version>
```

## Managing Data (Volumes/mounts):

```bash
docker volume --help: to get the volume help
docker volume create: to create a new volume
docker inspect volume: to inspect the created volume
docker run -v: to mount a volume

# Bind mount -> Run an image with a bound volume at /host in the container
docker run -it -v <absolute_path>:<folder path or new folder name> date_project:1.0
# Read only version uses ro flag <folder path or new folder name>:ro

# Volumes
docker volume create <volume name>
docker volume ls

# Mount volume and run container
docker run -it -v <volume name>:<folder path or new folder name> date_project:1.0
modify something in volume (eg. mkdir app)

# Run new container from same image with volume mounted
docker run -it -v <volume name>:<folder path or new folder name> --name second_container date_project:1.0
```

## Commands:

```bash
COPY, RUN and ADD create layers when building an image
```

## Dockerfile:

```dockerfile
FROM: #Invokes the base dependency (base image)
WORKDIR: #Sets a working directory for following commands (RUN and CMD)
ENV: Sets environment variables (export) setting ip to 0.0.0.0 permits access from host
COPY: #Copies from source to destination specified by WORKDIR
RUN: #Executes commands and commits the results (new layer to base image)
CMD: #Runs command inside container (only one per Dockerfile)
ENTRYPOINT: #permits configuring container as executable (override CMD)
```

## Building the dockerfile:

```bash
cd into directory
docker build -t flask_app:1.0 .
```

## Linking ports when running:

```bash
docker run -p 5000:5000 flask_app:1.0
```

## Daemon mode:

```bash
docker run -d -v <path_to_code_directory>:/code -p 5000:5000 flask_app:1.0
#prints SHA and container running in background
#access container with: docker exec -it <container> bash
```

## Container logs:

```bash
# view logs with: 
docker logs <container>
# save logs with redirection: 
docker logs <container> >output.log
```

## Real-Time logs:

```bash
# Gets realtime but exit will close container.
docker attach <container>
# Gets old logs and listens for new changes.
docker logs -f <container> 
```

## Troubleshooting:

```bash
# Space occupied by docker 
docker system df
# View specifics 
docker inspect <container/image/network>
```

