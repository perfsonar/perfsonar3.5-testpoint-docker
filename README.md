## perfSONAR Testpoint docker container

The docker container runs all perfSONAR Services in the "Testpoint" bundle, as described at:
http://docs.perfsonar.net/install_options.html

This can be used to run perfSONAR Testpoint services on any OS that supports docker.

Download the container:
>docker pull bltierney/perfsonar-testpoint-docker

To register your perfSONAR testpoint, start a container shell, and edit the file
/etc/perfsonar/lsregistrationdaemon.conf with the location and administrator information for your site.

If this host will be part of a centrally configured mesh, also edit the file 
/etc/perfsoanr/meshconfig-agent.conf, and update the 'configuration_url'.

>docker run -it bltierney/perfsonar-testpoint-docker /bin/bash

After editing the configuration files, exit the container and commit the change.
> docker commit -m "added config settings" containerID bltierney/perfsonar-testpoint-docker

Run the container:
>docker run -d -P --net=host -v /var/run bltierney/perfsonar-testpoint-docker

## Testing

Test the perfSONAR tools from another host with owamp and bwctl installed:
>owping hostname

>bwctl -c hostname

## Notes:
The perfSONAR hostname/IP is assumed to be the same as the base host. To use a different
name/IP for the perfSONAR container, see: https://docs.docker.com/articles/networking/

## Security:
make sure the following ports are allowed by the base host:
 pScheduler: 443, bwctl:4823, 5001-5900, 6001-6200 ; owamp:861, 8760-9960
See: http://www.perfsonar.net/deploy/security-considerations/


