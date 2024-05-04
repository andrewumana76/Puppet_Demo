# Installing Puppet on RHEL 9 Environment #

## Installing on Master Node ##

1. Login to the RHEL9 masternode
    * Hostname is already set to **masternode.ansibletest.demo**
    * DNS is already configured to reach/resolve multiple nodes

2. Add the Puppet Labs repo
    * **yum-config-manager --add-repo=https://yum.puppetlabs.com/puppet/el/9/x86_64/** 
    * set *gpgcheck=0* in /etc/yum.repos.d if needed  
3. Mount the BaseOS and AppStream repos from the RHEL 9 ISO and setup the repo file. I mount the ISO to /media/cdrom/

    * media.repo file:

        ![alt text](https://github.com/andrewumana76/Puppet_Demo/blob/main/pictures/media.repo.png)

    * yum.puppetlabs*.repo:  
  
        ![alt text](https://github.com/andrewumana76/Puppet_Demo/blob/main/pictures/yum.puppetlabs.repo.png)

5. **yum install puppet-release**
6. **yum install puppetserver**
7. **systemctl enable puppetserver && systemctl start puppetserver**
    * Enables and turns on puppet server  
8. **systemctl enable puppet && systemctl start puppet**
    * Enables and turns on puppet agent
9. **firewall-cmd --add-service=puppetmaster --permanent && firewall-cmd --reload**
    * Adds puppet service to the firewall
10. Add the puppet bin directory to path (if not there)
    * **env | grep PATH**

        ![alt text](https://github.com/andrewumana76/Puppet_Demo/blob/main/pictures/env_path.png)

    * If /opt/puppetlabs/bin is in the PATH, skip the next step
11. Need to change PATH in /etc/profile. /etc/profile is a system wide configuration file that is used for setting environment variables. If we only export in the current terminal, we will lose the environment variable after we close the session
    * **vi /etc/profile**
    * add *export PATH=$PATH:/opt/puppetlabs/bin* to the end of the file. Save and exit

        ![alt text](https://github.com/andrewumana76/Puppet_Demo/blob/main/pictures/etc_profile.png)
    * **source /etc/profile**  
12. Test the puppet server is running properly
   * **puppet agent --test --ca_server=masternode.ansibletest.demo**  
      * puppet command will not work if not in the PATH  
      * masternode.ansibletest.demo is my computer's hostname  
    

## Installing on Slave Node ##

1. Login to the RHEL9 slavenode
    * Hostname is already set to **ansiblenode.ansibletest.demo**
    * DNS is already configured to reach/resolve  to reach the masternode

2. Add the Puppet Labs repo
    * **yum-config-manager --add-repo=https://yum.puppetlabs.com/puppet/el/9/x86_64/** 
    * set *gpgcheck=0* in /etc/yum.repos.d if needed  
3. Mount the BaseOS and AppStream repos from the RHEL 9 ISO and setup the repo file. I mount the ISO to /media/cdrom/

    * media.repo file:

        ![alt text](https://github.com/andrewumana76/Puppet_Demo/blob/main/pictures/media.repo.png)

    * yum.puppetlabs*.repo:  
  
        ![alt text](https://github.com/andrewumana76/Puppet_Demo/blob/main/pictures/yum.puppetlabs.repo.png)

4. **yum install puppet-agent**
5. On the slave node, edit the /etc/puppetlabs/puppet/puppet.conf
   * puppet.conf:

      ![alt text](https://github.com/andrewumana76/Puppet_Demo/blob/main/pictures/slave_puppet_conf.png)

6. **systemctl enable puppet && systemctl start puppet**
7. **puppet agent -t**
   * This will create a connection between the agent and the server to generate a new certificate request

    ![alt text](https://github.com/andrewumana76/Puppet_Demo/blob/main/pictures/puppet_agent_t.png)

8. 

