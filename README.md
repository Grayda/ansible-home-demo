# ansible-home-demo

This is a sample ansible playbook for deploying my home server.

## Usage

1. Adjust `inventory.yaml` as needed
2. Create a file in the root of this folder called `credentials.txt` and put your SSH / becomes password in there
3. Run `bash install.sh`. This will install any necessary requirements, then run `playbooks/main.yaml`. You can pass it the name of a playbook (e.g. `bash install.sh homeassistant.yaml`) to just run that playbook.
4. If you want to add more services:
  - Create a folder in `files` (e.g. `files/glances`)
  - Place your `docker-compose.yaml` file in there with the `.j2` extension (e.g. `files/glances/docker-compose.yaml.j2`)
  - (Optional) create a file in the `vars` folder with the same folder name (e.g. `vars/glances.yaml`). You can do the same with the `vars/private` folder if you want to avoid checking in private info into git
  - Duplicate an existing playbook (e.g. `raneto.yaml`) and just change the `container` variable to match the folder name from before (e.g. `container: glances`)
  - Run `install.sh` against your new playbook (e.g. `bash install.sh glances.yaml`)

## About this demo

This demo will install Docker, dockge, Home Assistant, and Raneto. 

The `compose_dockge` role condenses a lot of code into something reusable which works fine for the majority of the Docker containers I'm deploying. It will create folders in `/home/yourusername/config` and `/home/yourusername/data`, render the `docker-compose.yaml.j2` file into `/opt/stacks`, and optionally, create additional user-specified folders (e.g. if you need to create folders to store stuff like pictures for Immich or roms for RomM)