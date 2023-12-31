Creating a README for deploying the Nethermind Lodestar client on Ubuntu 20.04 
---

# Deploying Nethermind Lodestar Client on Ubuntu 20.04

This README provides step-by-step instructions on how I deployed the Nethermind Lodestar client on a Ubuntu 20.04 machine following the documention on 
[Nethermind's site](https://docs.nethermind.io/nethermind/first-steps-with-nethermind/running-nethermind-post-merge). 
Nethermind is an Ethereum client implementation, and Lodestar is an Ethereum 2.0 Beacon Chain client.

**Note:** To follow along, ensure that you have administrative privileges or sudo access on your Ubuntu 20.04 server.

## Prerequisites

Before you begin, make sure you have the following prerequisites:

- Ubuntu 20.04 server with SSH access
- Internet connection
- Basic knowledge of Linux command line
- Administrative access or sudo privileges

## Step 1: Update and Upgrade

Start by updating the package list and upgrading installed packages:

```bash
sudo apt update
sudo apt upgrade
```

## Step 2: Install Nethermind

You'll need Node.js and npm (Node Package Manager) to run Lodestar. Install them using the following commands:

```bash
sudo add-apt-repository ppa:nethermindeth/nethermind
sudo apt install nethermind
nethermind --version
```

![nethermind-version](./images/nethermind-version.png)

## Step 2: Install Concensus client
This required installing git, docker and docker compose which I already had all but docker compose installed on my machine. I installed docker compose and went on to pull chainsafe Lodestar image

```bash
docker-compose --version`
```
![docker-compose](./images/docker-compose.png)


```bash
docker pull docker pull chainsafe/lodestar
```
![lodestar](./images/lodestar-pull.png)


## Step 3: Created a JWT secret file


```bash
openssl rand -hex 32 | tr -d "\n" > "/tmp/jwtsecret"
```
![lodestar](./images/lodestar.png)


## Step 4: Clone the Lodestar Repository

Clone the Lodestar repository from GitHub:

```bash
git clone https://github.com/ChainSafe/lodestar.git
cd lodestar-quickstart
```

## Step 4: Running Lodestar on Sepolia network

In the Lodestar directory type in the following command:

```bash
./setup.sh --dataDir --elClient nethermind --network sepolia --justCL --skipImagePull
./setup.sh --dataDir sepolia-data --elClient nethermind --network sepolia --justCL --skipImagePull --detached
```

## Step 5: Running Nethermind

Start Nethermind:

```bash
nethermind -c mainnet
```
This command is instructing Nethermind to start and use the configuration settings for connecting to the Ethereum mainnet

![nethermind](./images/nethermind-running.png)
![nethermind](./images/nethermind.png)
![nethermind](./images/stopped-nethermind.png)

