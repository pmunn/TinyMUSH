## TinyMUSH Docker README

### Quick Start
1. Copy the Dockerfile, compose.yaml, and entrypoint.sh into a folder to run from, e.g. ~/docker/tinymush/
2. Create a data/, data/db/, data/logs/, data/backups/, data/configs/, and data/docs/ folders.
3. Change the UID and GID values in the Dockerfile in two places and in compose.yaml in one place if the UID and GID you want it to run as aren't 1000.
4. Run "docker compose up -d" to start the server.
5. Run "telnet localhost 6250" to connect.

### Dockerfile
You may need to customize the UID and GID values in two places in the file.  The Dockerfile pulls the source from github and builds it in the first image, creates a second image, and copies the game files and supporting binaries into the second, which results in a smaller tinymush4 image.

### compose.yaml
Customize the UID and GID values to match the Dockerfile values.  It expects the following volume folders and runs on the default port 6250.
./data/db/
./data/logs/
./data/backups/
./data/configs/
./data/docs/

### entrypoint.sh
This script is used by the Dockerfile and copied into the container image so it runs when the container starts.  Each time the container starts, if either of these volume folders is empty, it will copy a set of default files into them:
./data/docs/
./data/configs/

This ensures the default set of files is put in place the first time it runs.  You can then customize them, and if you break your setup you can erase all the files in either of those folders and they will be reloaded with the default file set the next time the container runs.
