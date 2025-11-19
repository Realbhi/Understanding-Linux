### Step-by-step guide to get you from installing Docker Desktop on your Mac, to running an Ubuntu container. 

---

##  Step 1: Check system requirements

Before installing Docker Desktop, make sure your Mac meets the basic requirements. According to the official docs:

* A supported macOS version (current + two previous major releases) is required. 
* At least **4 GB of RAM** is required. 
* Virtualization support is needed (most modern Macs have it).

If your Mac meets these, you’re good to proceed.

---

##  Step 2: Download & install Docker Desktop

Here’s how to install it:

1. Go to the official Docker Desktop download page and get the macOS installer for your architecture (Intel or Apple silicon). 
2. Open the downloaded `.dmg` file, then drag the Docker icon into your **Applications** folder. 
3. Navigate to `Applications`, launch **Docker.app**. On first launch you may need to accept the license/terms and grant privileged access (for network components, symlinks) as prompted. 
4. Wait until the Docker whale icon in the menu bar stops showing “Starting…” and shows that Docker is running (often it becomes solid or shows status like “Docker Desktop is running”).

At this point the Docker daemon should be up and running.

---

## 🔍 Step 3: Verify installation

Open your Terminal and run:

```bash
docker --version
```

You should see something like `Docker version x.y.z, build ...`.
Then run:

```bash
docker info
```

You should get details about the Docker server, number of containers/images, etc. If you get an error like *“Cannot connect to the Docker daemon…”*, you’ll need to make sure Docker Desktop is indeed running and that your CLI can access the socket.

---

##  Step 4: Prepare the host folder you’ll bind-mount

Since you want to mount a host folder into the container (with `--mount type=bind,source=…,target=/data`), you need to create that folder first. For example:

```bash
cd ~/Downloads
mkdir ubuntu_data
```

Here `~/Downloads/ubuntu_data` will be your host folder. Make note of its full path (for example: `/Users/yourusername/Downloads/ubuntu_data`).

---

##  Step 5: Run the Ubuntu container

Now you’re ready to execute your `docker run` command. Adjusting it with the proper host folder path:

```bash
docker run -dit \
  --name ubuntu-container \
  --hostname ubuntu-dev \
  --restart unless-stopped \
  --cpus="2" \
  --memory="4g" \
  --mount type=bind,source="/Users/yourusername/Downloads/ubuntu_data",target=/data \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -p 2222:22 \
  -p 8080:80 \
  --env TZ=Asia/Kolkata \
  --env LANG=en_US.UTF-8 \
  ubuntu:latest /bin/bash
```

**Explanation of key parts:**

* `-dit`: Run container in detached interactive mode (so you get it running in background).
* `--name ubuntu-container`: Name it “ubuntu-container”.
* `--hostname ubuntu-dev`: Set the container’s hostname.
* `--restart unless-stopped`: Automatically restart unless you manually stop it.
* `--cpus="2"` & `--memory="4g"`: Limit CPU and memory usage.
* `--mount type=bind,source="…",target=/data`: This binds your host folder into the container at `/data`.
* `-v /var/run/docker.sock:/var/run/docker.sock`: Gives the container access to the Docker socket (for “Docker-in-Docker” type scenarios) — use with care.
* `-p 2222:22` & `-p 8080:80`: Map host ports 2222 → container port 22, and 8080 → container port 80.
* `--env TZ=Asia/Kolkata` & `--env LANG=en_US.UTF-8`: Set environment variables.
* `ubuntu:latest /bin/bash`: Use the latest Ubuntu image and start `/bin/bash`.

Before running, **double-check** that the `source` path is correct (your host folder) and that the ports 2222 and 8080 aren’t already in use on your Mac.

---

##  Step 6: Verify the container is running and access it

After running the command:

1. Check container status with:

   ```bash
   docker ps
   ```

   You should see your container “ubuntu-container” listed and `STATUS` should be “Up …”.
2. To get into the container’s shell:

   ```bash
   docker exec -it ubuntu-container /bin/bash
   ```

   This drops you into the container.
3. Verify `/data` folder (which should map your host folder) inside the container:

   ```bash
   ls /data
   ```

   You should see whatever you placed in `~/Downloads/ubuntu_data` on your host.
4. If you want to test port mapping:

   * Put a simple HTTP server in the container on port 80 (for example `apt update && apt install -y nginx` then start nginx) and then on the host visit `http://localhost:8080` to see if it’s reachable.

---

##  Step 7: Stopping and cleaning up

When you’re done:

* To stop the container:

  ```bash
  docker stop ubuntu-container
  ```
* To remove it (if you want to clean up):

  ```bash
  docker rm ubuntu-container
  ```
* If you also want to remove the image:

  ```bash
  docker rmi ubuntu:latest
  ```

