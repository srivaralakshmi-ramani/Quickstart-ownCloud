**Table of Contents:**
  - [Overview](#overview)
  - [Target audience](#target-audience)
  - [Scope of this document](#scope-of-this-document)
  - [Installation and configuration](#installation-and-configuration)
    - [Prerequisites](#prerequisites)
    - [Test the latest docker image](#test-the-latest-docker-image)
    - [Install and configure ownCloud server](#install-and-configure-owncloud-server)
  - [User Management](#user-management)
    - [Allow access to users](#allow-access-to-users)
    - [Add a user account](#add-a-user-account)
  - [Connect to ownCloud server](#connect-to-owncloud-server)
    - [Desktop client](#desktop-client)
    - [Mobile client](#mobile-client)
      - [Android](#android)
      - [iOS](#ios)
  
 ___

# Overview
ownCloud is an open-source client–server software for content collaboration. Using ownCloud you can create, manage, store, and share data and documents in real-time, seamlessly and simultaneously, from any compatible device and location. You can efficiently access, edit, monitor, sync, and comment on documents within the team and outside, in an easy, [secure](https://owncloud.com/product/security/) and productive manner.

- Visit https://owncloud.com/features/ for a complete list of features and capabilities of ownCloud.
- Visit [official ownCloud channel](https://www.youtube.com/channel/UC_4gez4lsWqciH-otOlXo5w) and [ownClouders community channel](https://www.youtube.com/channel/UCA8Ehsdu3KaxSz5KOcCgHbw) on YouTube for tutorials.
- Visit [doc.owncloud.org](https://doc.owncloud.org/) and [doc.owncloud.com](https://doc.owncloud.com/) for current editions of ownCloud manuals.

---

# Target audience
This document is intended for users with the following roles and describes procedures to perform the following tasks related to  the community edition of ownCloud server:
- **Administrator**
  - Install and configure an ownCloud server.
  - Allow access to connect to the ownCloud server, using the server's IP address and port number 8080.
  - Add a user account.
- **User**
  - Connect to the ownCloud server using a desktop or mobile client.
  
---

# Scope of this document
- **For procedures related to Administrator role:** This document provides information and instructions with its scope limited only to a quick, easy, and basic setup of the community edition of ownCloud server on a single Ubuntu 18.04 LTS machine, using a Docker image.

  This document assumes that you have already met the following conditions:
  - [Deployment Recommendations](https://doc.owncloud.com/server/10.5/admin_manual/installation/deployment_recommendations.html) and [System Requirements](https://doc.owncloud.com/server/10.5/admin_manual/installation/system_requirements.html).
  - A 64-bit version of Ubuntu 18.04 LTS operating system is installed with a Docker Engine and a Docker Compose CLI tool, on your local machine.

  > **Note:** This document does not cover the steps necessary for a detailed [manual installation](https://doc.owncloud.org/server/10.5/admin_manual/installation/manual_installation.html). If you are an experienced administrator who prefers a detailed manual installation and configuration, refer to the ownCloud's detailed [Admin Manual](https://doc.owncloud.org/server/10.5/admin_manual/installation/).
  
- **For procedures related to User role:** This document provides information and instructions with its scope limited only to quickly access the ownCloud server using a desktop client (Mac OS X and Windows) or mobile client (Android and iOS).

  - **For Mac OS X and Windows:** This document covers procedural information to install and configure a desktop client using only the [Installation Wizard](https://doc.owncloud.com/desktop/installing.html#installation-wizard).
  
  > **Note:** This document does not cover desktop client installation instructions specific to Linux distribution.

---

# Installation and configuration
You can install ownCloud using Docker and the official [ownCloud Docker image](https://hub.docker.com). This topic provides the following information for the minimal installation and basic configuration of the ownCloud server:
 - [Prerequisites](#prerequisites)
 - [Test the latest docker image](#test-the-latest-docker-image)
 - [Install and configure ownCloud server](#install-and-configure-owncloud-server)

## Prerequisites
1. Open the terminal, and execute the `lsb_release -a` command to verify that your Operating System version is [Ubuntu 18.04 LTS](https://releases.ubuntu.com/18.04/).

   You should see an output similar to this:
   ```bash
   $ lsb_release -a

   No LSB modules are available.
   Distributor ID: Ubuntu
   Description:    Ubuntu 18.04.3 LTS
   Release:        18.04
   Codename:       bionic
   ```
   >**Note:** The current official Docker image for ownCloud server is compatible only with Ubuntu 18.04.
   
2. Execute the `docker` command to verify that the docker is installed and running.

   You should see an output similar to this:
   ```bash
   $ docker

   Usage:	docker [OPTIONS] COMMAND

   A self-sufficient runtime for containers

   Options:
      --config string      Location of client config files (default "/home/srivaralakshmi/.docker")
      -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST env var and default context set with "docker context use")
      -D, --debug              Enable debug mode
      -H, --host list          Daemon socket(s) to connect to
      -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
          --tls                Use TLS; implied by --tlsverify
          --tlscacert string   Trust certs signed only by this CA (default "/home/srivaralakshmi/.docker/ca.pem")
          --tlscert string     Path to TLS certificate file (default "/home/srivaralakshmi/.docker/cert.pem")
          --tlskey string      Path to TLS key file (default "/home/srivaralakshmi/.docker/key.pem")
          --tlsverify          Use TLS and verify the remote
      -v, --version            Print version information and quit

    Management Commands:
    builder     Manage builds
    config      Manage Docker configs
    container   Manage containers
    context     Manage contexts
    engine      Manage the docker engine
    image       Manage images
    network     Manage networks
    node        Manage Swarm nodes
    ...
    ...
    ...
    ```


Visit [official docker documentation](https://docs.docker.com/engine/install/ubuntu/) for more information on the Docker Engine and its installation.

## Test the latest docker image
1. Download the [official docker image](https://hub.docker.com/r/owncloud/server/tags) for ownCloud server 10.5, by executing the following command:

   ```bash
   $ docker pull owncloud/server:10.5
   ```
   On successful download of newer image, the following status message is displayed:

   ```bash
   Status: Downloaded newer image for owncloud/server:10.5docker.io/owncloud/server:10.5
   ```
   >**Note:** The time taken to download the image from Docker Hub may vary depending on your connection speed.
   
2. (Optional) If you are denied permission to connect to the Docker daemon socket and get the following error message, execute the `sudo chmod 666 /var/run/docker .sock` command, enter your password on prompt, and retry downloading the docker image again:
   
   ```bash
   Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.39/containers/json: dial unix /var/run/docker.sock: connect: permission denied
   ```
   
3. Run the downloaded official docker image on port `8080` by executing the following command:
  
    ```bash
    $ docker run -p8080:8080 owncloud/server:10.5
    ```
   Wait until you see the following output:
   
    ```bash
    Starting apache daemon...
    ```
   
4. Enter `http://localhost:8080` in the address bar of your favorite browser. 
   Alternatively, you can enter `http://<public-IP-address>:8080`, the public IP address of the machine, if you have one.
   
   >**Tip:** Although the containers are up and running, it may still take a few minutes until onwCloud is fully functional. If you do not see the web page, check the logs displayed on the terminal. If you are using a remote server, try SSH tunneling.

   The login page of the ownCloud web UI is displayed, as shown in the following image:
   
   ![]{https://github.com/srivaralakshmi-ramani/ownCloud-Quickstart-Manual/blob/main/assets/docker_image_ownCloud_webUI_login_page.PNG}
   
   >**Note:** You do not have any valid user credentials, yet. As a result, you cannot use the docker image to log in to the ownCloud server.
   
4. Execute the following commands in the terminal to stop the container and remove it from your machine:

   ```bash
   $ docker ps -a
   CONTAINER ID        IMAGE                  COMMAND                  CREATED             STATUS              PORTS                    NAMES
   11f315a007b3        owncloud/server:10.5   "/usr/bin/entrypoint…"   29 minutes ago      Up 29 minutes       0.0.0.0:8080->8080/tcp   quirky_germain
    
   $ docker stop quirky_germain
   quirky_germain

   $ docker ps -a
   CONTAINER ID        IMAGE                  COMMAND                  CREATED             STATUS                        PORTS               NAMES
   11f315a007b3        owncloud/server:10.5   "/usr/bin/entrypoint…"   32 minutes ago      Exited (137) 51 seconds ago                       quirky_germain

   $ docker rm quirky_germain
   quirky_germain

   $ docker ps -a
   CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

   ```
   
   The testing of the latest official ownCloud Docker image is successful.
   
## Install and configure ownCloud server
1. Execute the following commands to create a project directory with the name `owncloud-docker-server` in your terminal and navigate to it:

    ```bash
    $ mkdir owncloud-docker-server
    $ cd owncloud-docker-server
    ```
    
2. Execute the following command to download the `docker-compose.yml` file from the GitHub repository of ownCLoud into your directory:

    ```bash
    $ wget https://raw.githubusercontent.com/owncloud/docs/master/modules/admin_manual/examples/installation/docker/docker-compose.yml
    ```
   You should see an output similar to this:
   
    ```bash
    --2020-11-29 17:04:30--  https://raw.githubusercontent.com/owncloud/docs/master/modules/admin_manual/examples/installation/docker/docker-compose.yml
    Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 151.101.112.133
    Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|151.101.112.133|:443... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 1650 (1.6K) [text/plain]
    Saving to: ‘docker-compose.yml’

    docker-compose.yml  100%[==================>]   1.61K  --.-KB/s    in 0s      

    2020-11-29 17:04:31 (9.21 MB/s) - ‘docker-compose.yml’ saved [1650/1650]
    ```
    You can notice that the `docker-compose.yml` file is now downloaded and saved in the `owncloud-docker-server` project directory.

3. Create a `.env` file using your favorite text editor and copy the following environment configuration settings in it:

    ```bash
    OWNCLOUD_VERSION=10.5
    OWNCLOUD_DOMAIN=localhost
    ADMIN_USERNAME=admin
    ADMIN_PASSWORD=admin
    HTTP_PORT=8080
    ```
    
4. Save the `.env` file in the `owncloud-docker-server` project directory.
5. Execute the `ls -a` command to verify that the `.env` file is now listed along with the docker-compose.yml file in the `owncloud-docker-server` project directory.

    ```bash
    ~/ownCloud-docker-server$ ls -a
    .  ..  docker-compose.yml  .env
    ```
    
6. Execute the `docker-compose up -d` command to build and start the container, using the `docker-compose` CLI tool.

    ```bash
    $ docker-compose up -d
    
    Creating network "ownclouddockerserver_default" with the default driver
    Creating volume "ownclouddockerserver_files" with local driver
    Creating volume "ownclouddockerserver_redis" with local driver
    Creating volume "ownclouddockerserver_backup" with local driver
    Creating volume "ownclouddockerserver_mysql" with local driver
    Pulling redis (webhippie/redis:latest)...
    latest: Pulling from webhippie/redis
    ae4a0e1e8235: Pull complete
    1e24c34b24d1: Pull complete
    95f9aef2e99d: Pull complete
    9641411ccde6: Pull complete
    3c5b5eddcd67: Pull complete
    Digest: sha256:42f6d51be6a7a5ef6fb672e98507824816566f0b1f89c19b2d585f54e26b2529
    Status: Downloaded newer image for webhippie/redis:latest
    Pulling db (webhippie/mariadb:latest)...
    latest: Pulling from webhippie/mariadb
    ae4a0e1e8235: Already exists
    1e24c34b24d1: Already exists
    95f9aef2e99d: Already exists
    bd3d546db57d: Pull complete
    ce65dc9183aa: Pull complete
    Digest: sha256:8a2c927529e5fd6238f08f79e3855d90a353e4475481574aa4bf0b90550b5db9
    Status: Downloaded newer image for webhippie/mariadb:latest
    Creating ownclouddockerserver_redis_1 ...
    Creating ownclouddockerserver_db_1 ...
    Creating ownclouddockerserver_redis_1
    Creating ownclouddockerserver_redis_1 ... done
    Creating ownclouddockerserver_owncloud_1 ...
    Creating ownclouddockerserver_owncloud_1 ... done
    ```
    
7. Execute the `docker-compose ps` command to verify whether all the containers have successfully started.

    ```bash
    $ docker-compose ps
             Name                            Command               State           Ports
     -------------------------------------------------------------------------------------------------
    ownclouddockerserver_db_1         /usr/bin/entrypoint /bin/s ...   Up      3306/tcp
    ownclouddockerserver_owncloud_1   /usr/bin/entrypoint /usr/b ...   Up      0.0.0.0:8080->8080/tcp
    ownclouddockerserver_redis_1      /usr/bin/entrypoint /bin/s ...   Up      6379/tcp
    ```
    
    You have successfully verified that the server is up and running.
8. (Optional) Execute the `docker-compose stop` command to stop the server.

The installation and basic configuration of the ownCloud server is complete.

Refer to [Installing with Docker](https://doc.owncloud.org/server/10.5/admin_manual/installation/docker/) for a complete information on managing a docker-based deployment.
>**Note:** The following procedures assume that as a prerequisite, you have the ownCloud server up and running with the default environment values.                                     
---

# User Management

## Allow access to users

## Add a user account

---

# Connect to ownCloud server

## Desktop client

## Mobile client

### Android

### iOS
