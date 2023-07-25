# Google Summer of Code 2022
A summary of my work during Google Summer of Code '22. I contributed to OWASP PurpleTeam during this period.


## Some issues faced :-

### Terminfo parse error – 

PurpleTeam CLI error, which makes the client terminal a blank screen, with the message “Terminfo Parse Error”. 
Fix: We have to set the environment variable called “TERM=xterm”. 
Known cause for this problem is CLI dependency blessed, is incompatible with the default TERM environment variable. 

### NodeJS dependency – 

We are given that we are allowed to use any version >= v12. 
Starting from v14, multiple versions were tried without success. 
Finally retried by installing node from scratch, using a package manager, got it working at NodeJS v18. 
There were permission issues while using Node that was installed using the “sudo apt install” method, even installing it to the root directory does not help. 
Used a package manager called “nvm” to install v18, permission issues were then solved, as this package managers installs node in its own subdirectory, thereby not messing up the permissions. 

### NodeGoat – 

This above package manager work around, causes a problem for installing NodeGoat, the System under Test for our paper, as “/home/node” is not created by the manager, which is required while installing. 
MongoDB v6 does not support some specific SQL manipulation queries that were implemented in NodeGoat. 
Fix: Use docker to install and restrict all NodeGoat dependencies, and match components appropriately.

### Docker issues – 

Installed the latest version of Docker, but this causes problems for a docker compose plugin. 
This is because while the latest Docker documentation installs docker compose v2 onto the system, the version supported by PurpleTeam “docker-compose-ui” is docker compose v1 both require different formats of commands to work in each version. 
Fix: A standalone version of docker compose v1 has to be installed alongside v2. 

### Docker compose bug – 

A docker-compose (.yml) file required by NodeGoat, does not follow the naming standards in the documentation, hence we are required to manually create a docker-compose.override.yml file and follow documentation for the file to be detected by Docker. 

### NODE_ENV – 

Issuing commands for PurpleTeam, requires that the NODE_ENV variable be set to local, as “NODE_ENV=local”, in the .bashrc file. 
This is the same file where we also define our variable TERM. 
After the variables have been set we can give the command 
“source ~/.bashrc” to update the source for terminal.


A preview of the purpleteam setup:

![alt text](https://github.com/shaneg07/GSoC-22/blob/main/assets/Preview1.jpg?raw=true)


https://gitlab.com/purpleteam-labs/purpleteam-labs-web
