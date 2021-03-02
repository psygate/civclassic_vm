# civclassic_vm
A simple vagrant vm setup for a vm resembling civclassic, enabling fast development.

# Important Things

**By running this setup you explicitly accept the minecraft server eula found in "eula.txt" in every minecraft server
folder.**

## Prerequisits

This setup assumes that the user has some familiarity with SSH, vagrant, git and command line utils on *nix.

## Usage

### Vagrant

*   Install virtualbox. `https://www.virtualbox.org/`

*   Install vagrant. `https://www.vagrantup.com/`

*   Create a directory `credentials` in the root of this project, and move your github ssh keys to the directory.
    The public key has to be in a file named `github.pub`  while the private key has to be in a file named `github`.

*   Open a shell in the root of this project and execute `vagrant up --provision`. This will setup a virtual development
    environment for you.
    
### Common Problems

#### Virtualbox & HyperV

Virtualbox may conflict with hyperV. Especially if you use Subsystem for Linux version 2 on windows. 

### Structure

#### `/projects`:
This folder contains all necessary subprojects cloned directly from the official github of civclassic. (`https://github.com/CivClassic/`)
You can modify those projects if you fork them on github and then set the remote of the git repository to your fork.

#### `/master_server`

This directory contains the files for the server instance on the master.

## Known errors

* Shared folders `projects` `master_server` do not exist:
  Switch to the folder with the Vagrant file is located (this should be the same as this README.md), type `vagrant up --provision` again.
  This should fix it. If it doesn't, `vagrant halt` and then `vagrant up --provision`.
  VBox is sometimes a bit stubborn about shared folder mounting.