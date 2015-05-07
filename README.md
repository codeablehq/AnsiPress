# AnsiPress - The most optimal server configuration for WordPress

Building servers can be hard, but from a system administrator’s point of view, WordPress servers are relatively easy to configure. AnsiPress aims to introduce some basic *Devops* knowledge to WordPress developers, and along the way, help them to automate server management.

## Install dependencies

First you need to have [Ansible](http://www.ansible.com) installed. It’s written in Python (which most operating systems already have), so let’s first install Python’s most popular package manager - *pip*:

```
$ sudo easy_install pip 
```

With *pip* installed, we can now use it to install Ansible:

```
$ sudo pip install ansible
```

You might want to try and update Ansible at this (optional) step:

```
$ sudo pip install -upgrade ansible
```

To verify it’s installed properly, run:

```
$ ansible —version
ansible 1.9.0.1
```

## How to use this script

There are two main playbooks: `setup.yml` and `first_run.yml`. The latter should only be ran once (but you can repeat it, of course, it just won’t have any effect, all of the tasks will be skipped). It’s purpose is to create a separate (non-root) user which will be used to login.

`setup.yml` holds all the necessary *roles* to set up the server.

Before you can run it, you need to copy `group_vars/example.yml`: Create a `production.yml` in the same directory and paste the contents of the `example.yml` in then modify them to your liking. 

Also, edit `inventories/production` and set the ip to point at your (empty) server.

To run the `first_run.yml`, enter the following command (-k asks for **SSH password**):

```
$ ansible-playbook first_run.yml -i inventories/production -k
``` 

Then run the `setup.yml` by entering (-K asks for **SUDO password**):

```
$ ansible-playbook setup.yml -i inventories/production -K
```

## Contribute!

The goal of this project is to gather as much knowledge from the community as possible in order to end up with a script that’ll build the most optimal WordPress server setup with a single command.

Fork it, fix it, create a pull request.

### License

AnsiPress is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, version 2.
