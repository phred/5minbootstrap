5minbootstrap
=============

Bootstrap and secure your server in 5 minutes flat.  A riff on this excellent post:

http://plusbryan.com/my-first-5-minutes-on-a-server-or-essential-security-for-linux-servers


There's a blog post that I wrote to go along with this.  Check it out!

http://practicalops.com/my-first-5-minutes-on-a-server.html


TL;DR
=====

## Step 1: Set the root password

Run:

    yourmachine$ ssh root@server


## Step 2: Fetch the bootstrap recipe

[https://github.com/phred/5minbootstrap/](https://github.com/phred/5minbootstrap/)

    yourmachine ~$ git clone https://github.com/phred/5minbootstrap.git
	yourmachine ~$ cd 5minbootstrap


## Step 3: Edit hosts.ini

Ansible needs to know about the servers you want to manage.  There is
no fancy central database, just a text file with a list of
servers.  Oh, it's called an "inventory file."

Edit the `hosts.ini` that came with the repository.  Replace
`127.0.0.1` with your IP address, and `:2222` with your SSH port.

    [newservers]
	127.0.0.1:2222
	

## Step 4: Update the SSH public key.

    yourmachine ~/5minbootstrap$ cp ~/.ssh/id_dsa.pub ./fred.pub

For simplicity I provided my public key in the repo.  Unless you want
to grant me login access to your server, you probably want to change
that. :-)


## Step 5: Run the playbook

This is the needed invocation *for Vagrant*:

    yourmachine ~/5minbootstrap$ ansible-playbook -i hosts.ini bootstrap.yml --ask-pass --sudo
	
If you are logging into a fresh Linode, or another sytem where you only have the `root` user, you need to run this command:

    yourmachine ~/5minbootstrap$ ansible-playbook -i hosts.ini bootstrap.yml --user root --ask-pass
	
## Step 6: Go get a cup of coffee because you're DONE.

I prefer hand-ground French pressed coffee myself.  Tea is also fine.

