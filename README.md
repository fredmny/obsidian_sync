# Obsidian self-hosted sync

This repository contains my configuration and details about what I am using to sync my Obsidian notes using a self-hosted database.

To use it I am using:
- The [Self-hosted LiveSync](https://github.com/vrtmrz/obsidian-livesync) Obsidian plugin
- CouchDB
- A domain
- Cloudflare tunnel
- AWS EC2
- Docker for the server and Cloudflared

## Obsidian LiveSync plugin

To connect to the database I am using the Obsidian [Self-hosted LiveSync](https://github.com/vrtmrz/obsidian-livesync) plugin by `vorotamoroz`. There are several ways to configure and host the database that are documented in the Plugin's repository. 

The option I used here is not documented there. I'll put a summarized description, but feel free to contact me and ask for more information.

## CouchDB

The database being used is the one suggested by the aforementioned plugin: [CouchDB](https://couchdb.apache.org/). This is being run within a Docker Container

## Domain

A domain is needed for the configuration with Cloudflare.

## Cloudflare Tunnel

I am using a Cloudflare tunnel to connect my subdomain to the AWS EC2 instance. With Cloudflare tunnels you do not need a static IP address, nor open ports in your router or subnet. The best explanation and configuration instruction I found so far is from NetworkChuck in [this video](https://youtu.be/ey4u7OUAF3c?si=9i3JYBwI7oepFSAQ)

The connection to the EC2 instance is being done using the official Docker image.

## AWS EC2

I am using a `t2.micro` EC2 instance running Ubuntu. So far it seems to offer enought resourcees. 

To install Docker just use [the official documentation](https://docs.docker.com/engine/install/ubuntu/)

## Docker

As already mentioned, CouchDB (database) and Cloudflared (to connect to the Cloudflare tunnel) are being run using Docker containers.

The `docker-compose.yml` file from this repository creates both containers from the official images. To configure it, you need two `.env` files with the configurations for each container with the variables mentioned below:
- `tunnel.env`:
    - `TUNNEL_TOKEN` - token supplied when creating the tunnel within Cloudflare's interfaces
- `couchdb.env`:
    - COUCHDB_USER - Admin user for CouchDB
    - COUCHDB_PASSWORD - Admin password for CouchDB
