<h1 align="center">Inception</h1>
<p align="center">
  <img src="https://img.shields.io/badge/grade-100%2F100-green?style=for-the-badge&logo=42&labelColor=gray"/>
</p>

<p align="center">
  <a href="https://github.com/pin3dev/42_Cursus/tree/main/library/#Inception">
    <img src="https://img.shields.io/badge/Docker-blue?style=for-the-badge"/>
    <img src="https://img.shields.io/badge/Containerization-blue?style=for-the-badge"/>
    <img src="https://img.shields.io/badge/Orchestration-blue?style=for-the-badge"/>
    <img src="https://img.shields.io/badge/Virtualization-blue?style=for-the-badge"/>
  </a>
</p>

<p align="center">
  <img src="https://github.com/pin3dev/42_Cursus/blob/a5d29b4a62cf51ed4d530307677175eb753b6afd/assets/Inception/Tutorial/Inception_Runing.gif" width="600" height="375" />
</p>

<h3>
  <p align="center">
    <a href="#introduction">Introduction</a> •
    <a href="#structure">Structure</a> •
    <a href="#cloning">Cloning</a> •
    <a href="#usage">Running</a> •
    <a href="#norms">Norms</a> •
    <a href="#theoretical">Theoretical</a> •   
    <a href="#tutorial">Tutorial</a>  
  </p>
</h3>

## 🗣️ Introduction <a id="introduction"></a>

The **Inception** project focuses on setting up a **multi-container** system using **Docker** and **Docker Compose**. The goal is to create a **virtualized infrastructure**, managing services like **NGINX, WordPress, and MariaDB**, while ensuring security and scalability. This project provides hands-on experience with **containerization, orchestration, and networking**.

## 🧬 Project Structure <a id="structure"></a>

The **Inception** project follows a modular architecture where each service runs inside its **own container**:

- **NGINX**: Serves as a reverse proxy and handles SSL/TLS encryption.
- **WordPress**: A PHP-based CMS running with php-fpm.
- **MariaDB**: A MySQL-compatible database engine.
- **Docker Compose**: Manages the orchestration of all containers.
- **Volumes**: Persistent storage for WordPress and the database.

<!--
## 🗃️ Documentation <a id="docs"></a>

For detailed documentation, including usage examples and function breakdowns, please visit the link below:

<p align="center">
  <a href="https://github.com/pin3dev/42_Inception/wiki">
    <img src="https://img.shields.io/badge/Inception_Docs-lightgreen?style=for-the-badge"/>
  </a>
</p>
-->

## 🫥 Cloning the Repository <a id="cloning"></a>

To clone and set up the project, run the following commands:

```bash
git clone https://github.com/pin3dev/42_Inception.git
cd 42_Inception/root
```   
This will download the project from GitHub into your local machine. Once inside the 42_Inception directory, you can run the project using the provided Makefile.

## 🕹️ Running the Project <a id="usage"></a>

### Makefile

A `Makefile` is provided to simplify the running process. The Makefile includes the following rules:

- **`build`**: Builds the Docker containers.
- **`run`**: Starts the Docker containers in detached mode.
- **`exec <docker name>`**: Opens an interactive shell inside a running container.
- **`status`**: Displays logs of a specific container.
- **`stop`**: Stops and removes all running containers.
- **`iclean`**: Stops and removes containers along with all built images.
- **`vclean`**: Removes containers, images, and volumes.
- **`fclean`**: Performs a full cleanup, removing all unused containers, images, and volumes.
- **`dls`**: Lists all Docker containers.
- **`vls`**: Lists all Docker volumes.
- **`ils`**: Lists all Docker images.
- **`nls`**: Lists all Docker networks.

To build and run the containers, execute:

```bash
make
```

To stop and clean up the containers:
```bash
make fclean
```

### Basic Tests

With the containers running you can run the tests below:

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

## ⚠️ Norms and Guidelines <a id="norms"></a>

This project strictly follows the [**42 School Norm**](https://github.com/pin3dev/42_Cursus/blob/b9cd0fe844ddb441d0b3efb98abcee92aee49535/assets/General/norme.en.pdf) coding guidelines, which significantly influenced certain decisions in its implementation. These rules may sometimes lead to seemingly inefficient or unusual solutions, but they were necessary to meet the strict requirements of the school. 

## 📚 Theoretical Background <a id="theoretical"></a>

All the theoretical material used to develop this project is organized and can be accessed directly via the link below:

<p align="center">
  <a href="https://github.com/pin3dev/42_Cursus/blob/main/library/README.md#05-inception">
    <img src="https://img.shields.io/badge/Inception_Library-gray?style=for-the-badge"/>
  </a>
</p>

## 🔬 Tutorial <a id="tutorial"></a>

A step-by-step tutorial is available and can be followed to complete the project. It is linked in the button below.

<p align="center">
  <a href="https://github.com/pin3dev/42_Inception/wiki">
    <img src="https://img.shields.io/badge/Inception_Tutorial-lightgreen?style=for-the-badge"/>
  </a>
</p>

