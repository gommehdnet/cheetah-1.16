#Cheetah
## High-performance fork of PaperSpigot

This is a fork of https://github.com/PaperMC/Paper for Minecraft 1.16.5. It aims to improve the general stability and performance of the Minecraft server.

### Artifacts

We do not offer 

### How to initialize
* Clone this repository
* `git submodule init`
* `git submodule update`
* `./cheetah up`
* `./cheetah patch`

### How to build
Simply run `mvn clean install` from the root directory. After this, you will find the bundled jar file in Cheetah-Server/target.
### Creating a patch

First, patch the project as described above. Then, edit the server source code in the respective subdirectory (e.g. Paper-Server, Paper-Api).
After you completed your changes, commit them with the subdirectory as your current working directory (e.g cd Paper-Server && git add foo.txt instead of git add PaperServer/foo.txt). 
Finally, rebuild the patches by running `/cheetah rb` in the root directory.
### Contributions

Please submit pull requests directly to the upstream: https://github.com/PaperMC/Paper