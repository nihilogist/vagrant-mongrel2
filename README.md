# vagrant-mongrel2
## A simple Vagrantfile to provision a mongrel2 server
This repository is a simple Vagrant file that will start up a single Ubuntu virtual machine and install the mongrel2 webserver onto it. It starts the most basic of the mongrel2 example applications, and maps the port 6767 from the guest machine to port 6767 on the host to allow easy checking of when the server is active.
Should be relatively easy to then expand on this to add better provisioning of the server.
