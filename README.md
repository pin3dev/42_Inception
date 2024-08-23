# Inception `100/100`


<p align="center">
  <img src="https://github.com/pin3dev/42_Cursus/blob/a5d29b4a62cf51ed4d530307677175eb753b6afd/assets/Inception/Tutorial/Inception_Runing.gif" width="600" height="375" />
</p>

<p align="center">
  <a href="https://github.com/pin3dev/42_Inception/wiki">🚢---TUTORIAL---🚢</a>
</p>


## Table of Contents
- [Project Overview](#overview)
- [Guidelines](#guidelines)
- [Mandatory Features](#features)
- [Execution](#execution)
- [To Study](#links-to-study)

## Overview
The `Inception` project involves setting up a small infrastructure using Docker and Docker Compose within a Virtual Machine, with a focus on learning how to manage multiple services—such as NGINX, WordPress, and MariaDB—each running in dedicated containers, all orchestrated by Docker Compose.
  
## Guidelines

### Setup and Structure:

- All project files must be inside a `srcs` directory.
- A `Makefile` is required at the root level to build and run the entire application.
- Use Docker Compose to manage your services, with each service having its own `Dockerfile`.
- Containers should use the latest stable version of `Alpine` or `Debian`.

### Forbidden:

- Using `pre-built` Docker images from Docker Hub.
- `Infinite loops` or hacky patches in the entrypoint of the Dockerfile.
- Storing `passwords` or `sensitive information` directly in Dockerfiles.

### Allowed:

- Environment variables stored in a `.env` file.
- `Docker secrets` for managing sensitive data.
- Custom domain setup, e.g., `login.42.fr`, pointing to your `local IP`.

## Features
- **NGINX service**: Configured with TLSv1.2 or TLSv1.3.
- **WordPress service**: Running with php-fpm, without NGINX.
- **MariaDB service**: Configured separately, without NGINX.
- TLS/SSL configured via NGINX as the single entry point through port `443`.
- Dedicated `volumes` for WordPress files and database.

## Execution
To build and run the project, navigate to the root directory and run:
```bash
make
```

## Tests
**TLS/SSL:**
```bash
openssl s_client -connect localhost:443
# Look in the output for the line with “Protocol” followed by the type of protocol used
# If you try any other port, the output should be an error
```

**PORTS:**  
**nginx connects to wordpress via port 9000**
```bash
docker exec -it nginx nc -zv wordpress 9000
# [SUCCESS MESSAGE]: Connection to wordpress (xxx.x.x.x) 9000 port [tcp/*] succeeded!
# [ERROR MESSAGE]: OCI runtime exec failed: exec failed: unable to start container process: exec: "nc"...
# If the error occurs, it means netcat isn't installed in the Docker container. To resolve this, run:
docker exec -it nginx bash
apt-get update && apt-get install -y netcat
docker exec -it nginx nc -zv wordpress 9000
exit
# Now, try the initial command again:
docker exec -it nginx nc -zv wordpress 9000
```

**wordpress connects to mariadb via port 3306**
```bash
docker exec -it wordpress nc -zv mariadb 3306
# [SUCCESS MESSAGE]: Connection to mariadb (xxx.x.x.x) 3306 port [tcp/mysql] succeeded!
# [ERROR MESSAGE]: OCI runtime exec failed: exec failed: unable to start container process: exec: "nc"...
# If the error occurs, it means netcat isn't installed in the Docker container. To resolve this, run:
docker exec -it wordpress bash
apt-get update && apt-get install -y netcat
docker exec -it wordpress nc -zv mariadb 3306
exit
# Now, try the initial command again:
docker exec -it wordpress nc -zv mariadb 3306
```

**MARIADB:**
```bash
docker exec -it mariadb bash
mariadb
SHOW DATABASES;
USE <database_name>;
SHOW TABLES;
SELECT * FROM <table_name>;
```

## Links to Study
| Grade | Lang | Type | Links and Subjects |
|:----:|:----:|:----:|:------------------|
| ⭐  |  🇺🇸 | 🔖  | [Debian Versions](https://www.debian.org/releases/) |  
|  ✅ |  🇺🇸 |  📚 | [Docker Concepts](https://container.training/intro-selfpaced.yml.html#1) |  
| ⭐⭐ |  🇺🇸 |  📄 | [42 Inception Guide - Part 1](https://medium.com/@ssterdev/inception-guide-42-project-part-i-7e3af15eb671) |  
| ⭐⭐ |  🇺🇸 |  📄 | [42 Inception Guide - Part 2](https://medium.com/@ssterdev/inception-42-project-part-ii-19a06962cf3b) |  

> ✅ OK | ⭐ Good | ⭐⭐ VeryGood | 🤩 Amazing | 🔖 Bookmarked2Read  
> 📄 Blog | 💭 Chat | 📹 Video | 📚 Book & Scientific Papers   
