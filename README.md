# The-value-and-use-of-containers

Docker and Singularity are container engines which can be used to deploy software packages in a lightweight, standalone, reproducible environment. Using containers, software is packaged with its dependencies and is isolated from the host machine. This ensures software runs uniformly regardless of infrastructure.

## Useful Definitions

### Dockerfile ###
A Dockerfile is text file which provides instructions to Docker on how to build a Docker image.

### Singularity recipe ###
A Singularity recipe is text file which provides instructions to Singularity on how to build a Singularity image.

### Images ###
Images act as a snapshot of a container that Docker can build upon. They contain the software and its dependencies.

### Containers ###
At runtime images become containers.

### Volumes ###
Volumes are used to mount data in Docker so it can be accessed by a container.

## Docker ##

### Working with Docker Hub ###

Search Docker Hub for images
```
docker search $searchterm
```
Download an image from Docker Hub
```
docker pull $repository:tag
```
Pull an image from quay.io
```
docker pull quay.io/$repository:tag
```

### Finding Image and Container Information ###
List all running containers
```
docker ps
```
List all containers and their status
```
docker ps -a
```
List all downloaded images
```
docker images
```

### Working with Images and Containers ###
Build an image from a Dockerfile
```
docker build -t $imagename -f path/to/Dockerfile .
```
Run an image, creating a container
```
docker run $imagename $command
```
Run an image, while attaching a volume
```
docker run -v /absolute/path/to/files:/path/in/container $imagename $command
```
Run an image with an interactive terminal
```
docker run -it $imagename bash
```
Run an image, and delete the container once it's stopped running
```
docker run --rm $imagename $command
```
Start/stop a container
```
docker start/stop $containerid
```

### Deleting Images and Containers ###
Delete a container
```
docker rm $containerid
```

Delete an image
```
docker rmi $imagename
```

Delete all stopped containers
```
docker container prune
```

Remove dangling images
```
docker image prune
```

### Working with volumes ###
Volumes are used to manage data in Docker. By default the data in a container will not persist when the container is destroyed. As such we store our input and output files for the containerized software in a directory on the host machine, which we attach as a volume. So even when the container is stopped the files will persist.

We can attach a host volume to any directory in the container using the -v flag. Note that when attaching a volume you must provide Docker with the absolute (full) path.
```
docker run -v /absolute/path/to/directory/on/host:/path/to/directory/in/container $imagename $command
```

## Singularity ##

### Downloading images for Singularity ###

Singularity images take the form of .sif files. As well as pulling images from Singularity container registries, Singularity can also pull Docker images from Docker Hub and convert them to Singularity images.

Singularity can interact with many container registires:
* Singularity Container Library (Sylabs)
* Docker Hub
* Singularity Hub (no longer being updated, archive only)
* Quay.io

Pulling an image from the Singularity Container Library
```
singularity pull library://$repository:tag
```
Pulling an image from Docker Hub
```
singularity pull docker://$repository:tag
```
Pulling an image from quay.io
```
singularity pull docker://quay.io/$repository:tag
```

### Working with Images and Containers ###
To enter a container
```
singularity shell $image.sif
```
To run commands within the container from the host
```
singularity exec $image.sif $command
```
To execute the runscript of a container
```
singularity run $image.sif
```
