# Installing Puppet on RHEL 9 Environment#

1. Login to the RHEL9 masternode
2. Add the Puppet Labs repo
* yum-config-manager --add-repo=https://yum.puppetlabs.com/el/9/x86_64/  
* set *gpgcheck=0* in /etc/yum.repos.d if needed  
3. Mount the BaseOS and AppStream repos from the RHEL 9 ISO and setup the repo file. I mount the ISO to /media/cdrom/

* media.repo file:

    ![alt text](https://github.com/andrewumana76/Puppet_Demo/blob/main/pictures/media.repo.png)


5. yum install puppet-release
