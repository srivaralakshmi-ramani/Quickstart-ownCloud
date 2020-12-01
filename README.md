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
1. Open the terminal, and run the `lsb_release -a` command to verify that your Operating System version is [Ubuntu 18.04 LTS](https://releases.ubuntu.com/18.04/).

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
   
2. Run the `docker` command to verify that the docker is installed and running. You should see an output similar to this:

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
## Install and configure ownCloud server


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
