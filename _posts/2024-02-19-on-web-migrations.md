---
title : "My experience migrating web-servers"
layout : post
categories : servers web linux
---

First off, migrations are only as easy as you made them to start.

If a server/service is built with duct tape without version control. It's going to take a lot longer.

Thankfully for the most part I didn't do that.

However what I did have was about 10 different web platforms that I had built using a variety of technologies scattered with different versions across 8 servers. (Some servers I discovered were not being used at all).

The main cause was I would need to make a revision for a specific client, which would break/change things for other clients. Rather than making a fundamental change, I just cloned the repository to a new server I would bill to the client with their own specific features.

But now, I want to have everything be centralized on one server. Not just to lower costs, but also to centralize control. 

By hosting on a single server I can
1. Scale the server if needed
2. Not pay for a new server for a small project that won't be going anywhere
3. Have all security/firewall settings be standardized and setup
4. Faster launch for new services
6. Backups backups backups. With a single server I can do daily backups of all the databases, and then even have a snapshot that I can revert to if everything breaks.

The most important reason for me, is just to avoid mistakes. The first couple of servers and web services I setup were "Ransomed" by some bot that just attemped to connect to every MongoDB instance, and unfortunatly for me I had not setup authenication correctly.

Since then I have changed methods to hosting the DB on a docker instance that is only availible locally, and blocked off from the firewall. All the firewall does is SSH/HTTP (to be able to grab SSL Certs)/HTTPS. If another service is temporaraly needed, then I can just use an SSH tunnel to access it.

Anyways, the first step I did was reconnaissance. I went through every server, saw what services were needed, as well as what "web services"/"platforms" it was running

Once I had that I started with priority, which happened to be my newest projects/easiest to migrate. As simple as a git clone and yarn install. But then I needed to import my old databases. I found this amazing article on [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-back-up-restore-and-migrate-a-mongodb-database-on-ubuntu-20-04) which walks you through the whole process (as well as setting up backups and deleting backups older than 7 days with cron jobs).

The whole migration process per web service pretty much looked like this:
1. Clone code base on new server
2. Install packages
3. Copy over .env files, and modify to connect to existing services (Redis/Mongodb Docker)
4. On old server, use mongodump
5. Zip the export, download it locally to my NAS for backup
6. Move Zip to new server, unzip, and use mongorestore
7. Start new services
8. Point domains to new server
9. Setup new domain in /etc/nginx/sites-availible
10. Setup link with ```sudo ln -ls /etc/nginx/sites-availible/domain.url /etc/nginx/sites-enabled```
11. Use ``` sudo certbot --nginx``` to get new SSL Certs
12. And voiala!

I have not finished migrating everything yet, but should be done by the end of the week.

The peace of mind that I have acieved by having everything centralized is priceless. And I am excited to use this new setup/workflow to rapidly prototype and deploy new projects!


