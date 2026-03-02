#### DOCKER

- A **containerization software** that allows us to isolate software
- You create containers and what is running inside that container doesn't affect the rest of the machine
- **Docker Image** --> a snapshot of a container that we can define to run our software, or in this case our data pipelines
##### Main Components

1. **Images** --> contains all the ingredients and instructions
	- a complete snapshot of the OS
	- contains
		- technologies we need
		- runtimes
		- the tools/instructions to run our code
	- when we do `docker run`, we use this image to create a **container**
		- this container contains exactly what's in the image

2. **Containers** --> isolated copy of a docker image
	- they're stateless, they do NOT preserve state or store anything we run inside them
	- any changes done inside a container will NOT be saved when the container is killed and started again
##### Advantages

- **Reproducibility** --> same environment everywhere
- **Isolation** --> apps run independently
- **Portability** --> run anywhere Docker is installed

---
#### COMMANDS
##### Basic Commands

- Check Docker version:
> [!NOTE]
> ```bash
> docker --version
> ```
##### Running Containers From Images

- Run a container from a docker image (`python3`):
	- `-slim`--> provides a smaller Python version
> [!NOTE]
> ```bash
> docker run python:3.13.11-slim
> ```
- To enter a container, run it in `-it` mode:
	- `-i`--> interactive
		- keeps the connection open
		- tells docker to listen to your keyboard
	- `-t`--> TTY
		- gives you a terminal screen
		- makes the container look like a real Linux window
> [!NOTE]
> ```bash
> docker run -it ubuntu
> ```
- Override the default command of an image:
	- `--entrypoint`--> lets you hijack the default image command and run something else instead
> [!NOTE]
> ```bash
> docker run -it --entrypoint=bash python:3.13.11-slim
> ```
##### Managing Containers

- See all container that we ran before:
> [!NOTE]
> ```bash
> docker ps -a
> ```
> 
- Get container IDs:
	- `-a`--> finds all the container IDs
	- `-q`--> shows only the quiet version (just the IDs, no extra text)
> [!NOTE]
> ```bash
> docker ps -aq
> ```
- Delete a container (in Bash):
> [!NOTE]
> ```bash
> docker rm `docker ps -aq`
> ```
- Delete a container (in PowerShell):
> [!NOTE]
> ```powershell
> docker rm $(docker ps -aq)
> ```
- Delete a container after exiting it immediately:
> [!NOTE]
> ```bash
> docker run -it --rm ubuntu
> ```
##### Volumes (Bind Mount)

- It creates a **live bridge** between your actual computer and your container
- Anything you change on your host machine, instantly shows up in the container

- Map a directory on your host machine to a container:
	- `-v`--> volume
		- connects a folder on your host machine to a folder inside a docker container
	- `\`--> line continuation character
	- before `:`--> source (on the host machine)
	- after `:`--> destination (inside the container)
> [!NOTE]
> ```bash
> docker run -it \
>     --rm \
>     -v "<path-on-host>:<path-in-container>" \
>     --entrypoint=bash \
>     python:3.13.11-slim
> ```

---
