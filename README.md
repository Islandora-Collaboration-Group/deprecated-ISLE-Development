# ISLE Docker Development Repo
Development repo for testing.  
NOT FOR PRODUCTION!

Docker Image GitHub Repos that comprise this stack: 
 - [`isle-tomcat`](https://github.com/Islandora-Collaboration-Group/isle-tomcat/) (base image)
 - [`isle-fedora`](https://github.com/Islandora-Collaboration-Group/isle-fedora/)
 - [`isle-solr`](https://github.com/Islandora-Collaboration-Group/isle-solr/)
 - [`isle-apache`](https://github.com/Islandora-Collaboration-Group/isle-apache/)
 - [`isle-imageservices`](https://github.com/Islandora-Collaboration-Group/isle-imageservices/)

## Requirements  
* Docker-CE or EE
* Docker-compose
* Git
* Time required > 30 minutes.

## Quick Start
1. Clone this repo <!-- OR wget the docker-compose.yml -->
    - `git clone https://github.com/Islandora-Collaboration-Group/ISLE-Development.git` 
    <!-- - `wget https://github.com/Islandora-Collaboration-Group/ISLE-Development/blob/development/docker-compose.yml` -->
<!-- 1. Clone this repository recursively. In terminal:
    - `git clone --recurse-submodules https://github.com/Islandora-Collaboration-Group/ISLE-Development.git`
2. Change directory to the cloned directory:
    - `cd ISLE-development` (by default)
3. Build the tomcat-base image locally:
    - `docker build -t isle-tomcat:latest --rm images/isle-tomcat/` 
4. When isle-tomcat is complete, build the rest of the refactored stack:
    - `docker-compose build` -->
2. Change directory to the cloned directory:
    - `cd ISLE-development` (by default)
    <!-- - create a folder and move the docker-compose.yml there! -->
3. Pull the latest images:
    - `docker-compose pull`
4. Launch the ISLE preRC stack for testing:
    - `docker-compose up -d`
5. Install Islandora on the isle-apache-ld container:
    - `docker exec -it isle-apache-ld bash /utility-scripts/isle_drupal_build_tools/isle_islandora_installer.sh`
6. To wrap up testing:
    - In the folder with the docker-compose.yml `docker-compose down -v`


## Important Notes, Ports, Pages and Usernames/Passwords
@SEE: https://github.com/Islandora-Collaboration-Group/ISLE  
There are additional steps such as adding isle-localdomain to your etc/hosts which will not be covered here. 

### Locations, Ports:
* Make sure your /etc/hosts points isle.localdomain to 127.0.0.1. See original docs on how-to.
* Islandora is available at http://isle.localdomain
  * **You may need to point directly to the IP address of isle-apache, here's how:**
    - `docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' isle-apache-ld`
    - Copy the IP and browse to it.  `http://{IP}/`
* Traefik is available at http://admin.isle.localdomain OR http://localhost:8080/
* Fedora is available at http://isle.localdomain/fedora OR http://localhost:8081/
* Solr is available at http://isle.localdomain/solr OR http://localhost:8082/
* Image Services are available at http://images.isle.localdomain OR http://localhost:8083/


### Users and Passwords
Read as username:password

Islandora (Drupal) user and pass (default):
 * `isle`:`isle`

All Tomcat services come with the default users and passwords:
* `admin`:`isle_admin`
* `manager`:`isle_manager`
