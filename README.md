# ansible-home-demo

This is a sample ansible playbook for deploying my home server.

## Usage

1. Install ansible. Instructions can be found on the [Ansible website](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#pipx-install). If using Windows, you need to set up ansible using WSL2.
2. Download and extract or clone this repository (e.g. `git clone https://github.com/grayda/ansible-home-demo`)
3. Change the IP address in `inventory.yaml` to match your remote machine (i.e. the machine you are setting up, _not_ the machine you are running ansible on)
4. Create a file in the root of this folder called `credentials.txt` and put your SSH password in there
5. Run `bash install.sh`. This will install any necessary requirements, then it will run `playbooks/main.yaml`. You can pass it the name of a playbook (e.g. `bash install.sh homeassistant.yaml`) to just run that playbook.

## Adding more services
1. Create a new folder in the `files` folder (e.g. `files/glances/`)
2. Place your `docker-compose.yaml` file in that folder, and append `.j2` to the filename (e.g. `files/glances/docker-compose.yaml.j2`)
3. Create a file in the `vars` folder with the same name as the folder (e.g. `files/glances.yaml`). These variables can be used in your `.j2` files. See the [Ansible documentation on variables](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_variables.html#referencing-simple-variables)
4. Duplicate an existing playbook (e.g. `playbooks/homeassistant.yaml`), rename it (e.g. `playbooks/glances.yaml`) and change as necessary.
5. Edit `playbooks/main.yaml` and add a new section, similar to the other ones in the file
6. Run `bash install.sh`. This will add the new docker container (stopped). You just need to start the container using dockge or whatever your preferred container management system is. 

## About this demo

This demo will install Docker, dockge, Home Assistant, and Raneto. 

The `compose_dockge` role condenses a lot of code into something reusable which works fine for the majority of the Docker containers I'm deploying. It will create folders in `/home/yourusername/config` and `/home/yourusername/data`, render the `docker-compose.yaml.j2` file into `/opt/stacks`, and optionally, create additional user-specified folders (e.g. if you need to create folders to store stuff like pictures for Immich or roms for RomM)
