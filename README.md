# ISLE Docker Development Repo
Development repo for testing.

IMAGES REFACTORED: [`isle-tomcat`](https://github.com/Islandora-Collaboration-Group/isle-tomcat/) (new base image), [`isle-fedora`](https://github.com/Islandora-Collaboration-Group/isle-fedora/), [`isle-solr`](https://github.com/Islandora-Collaboration-Group/isle-solr/).  
IMAGES QUEUED: isle-apache, isle-proxy.  
NEW IMAGES QUEUED: isle-imageservices.

## Requirements  
* Docker-CE or EE
* Docker-compose
* Time required > 90 minutes.

## How to build and run development images.  
1. Clone this repository recursively. In terminal:
    - `git clone --recurse-submodules https://github.com/Islandora-Collaboration-Group/ISLE-Development.git`
2. Change directory to the cloned directory:
    - `cd ISLE-development` (by default)
3. Build the tomcat-base image locally:
    - `docker build -t isle-tomcat:latest --rm images/isle-tomcat/` 
4. When isle-tomcat is complete, build the rest of the refactored stack:
    - `docker-compose build`
5. When the build has completed, launch the ISLE stack for testing:
    - `docker-compose up -d`
6. Install Islandora on the isle-apache-ld container:
    - `docker exec -it isle-apache-ld bash /tmp/isle_drupal_build_tools/install_isle_ld_site.sh`


## Important Notes, Ports, Pages and Usernames/Passwords
@SEE: https://github.com/Islandora-Collaboration-Group/ISLE  
There are additional steps such as adding isle-localdomain to your etc/hosts which will not be covered here. 

Note that some images are unrefactored yet, and may not cooperate in the new stack. isle-proxy and isle-apache remain.

### Locations, Ports:
* Islandora is available at http://localhost:80/
  * Note this is being routed through proxy which is unrefactored. 
  * **You may need to point directly to the IP address of isle-apache, here's how:**
    - `docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' isle-apache-ld`
    - Copy the IP and browse to it.  `http://{IP}/`
* Fedora is available at http://localhost:8080/
* Solr is available at http://localhost:8091/

### Users and Passwords
Read as username:password

All Tomcat services come with the default users and passwords:
* `admin`:`isle_admin`
* `manager`:`isle_manager`

Islandora user and pass (default):
 * `isle_localdomain_admin`:`isle_localdomain_adminpw2018`
