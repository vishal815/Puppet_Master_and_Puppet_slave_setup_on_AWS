
# Puppet Master and Puppet Agent Setup on AWS

This guide will help you set up a Puppet Master and Puppet Agent (or Puppet Node) on Amazon Web Services (AWS) using straightforward commands. This setup allows you to manage configurations and automate tasks on your nodes using Puppet.

## Puppet Master Setup

### Modify the Puppet Master's hosts file

```
sudo nano /etc/hosts
```

Add the following line:

```
<Puppet_Master_Private_IP> puppet
```

### Download and install the Puppet Master packages

```
curl -O https://apt.puppetlabs.com/puppet6-release-bionic.deb
sudo dpkg -i puppet6-release-bionic.deb
sudo apt-get update
sudo apt-get install puppetserver -y
```

### Allow traffic on port 8140

```
sudo ufw allow 8140
```

### Configure and start Puppet Master

```
sudo systemctl enable puppetserver.service
sudo systemctl start puppetserver.service
```

### Verify the version of Puppet Master

```
sudo systemctl status puppetserver.service
```

## Puppet Agent Setup

### Modify the Puppet Agent's hosts file

```
sudo nano /etc/hosts
```

Add the following line:

```
<Puppet_Master_Private_IP> puppet
```

### Download and install the Puppet Agent packages

```
curl -O https://apt.puppetlabs.com/puppet6-release-bionic.deb
sudo dpkg -i puppet6-release-bionic.deb
sudo apt-get update
sudo apt-get install puppet-agent -y
```

### Enable and restart the Puppet Agent service

```
sudo systemctl enable puppet
sudo systemctl restart puppet
sudo systemctl status puppet
```

## Signing Certificates on the Puppet Master

### List certificate requests

```
sudo /opt/puppetlabs/bin/puppetserver ca list
```

### Sign a specific certificate request

```
sudo /opt/puppetlabs/bin/puppetserver ca sign --certname <Agent_CertName>
```

## Applying Manifests on Puppet Agent

### Create a Puppet manifest file

```
sudo nano /etc/puppetlabs/code/environments/production/manifests/site.pp
```

Add content like the following example:

```
file { '/tmp/puppet_test.txt':
  ensure => present,
  mode   => '0644',
  content => "Hello from Puppet master (Welcome to puppet testing with vishal.) to agent on IP address ${ipaddress_eth0}\n",
}
```

### Trigger Puppet Agent to apply the changes (run on puppet Agent)

```
sudo /opt/puppetlabs/bin/puppet agent --test
```

### Check the content of the test file (run on puppet Agent)

```
sudo cat /tmp/puppet_test.txt

```
# 👉
[PPT](https://github.com/vishal815/Puppet_Master_and_Puppet_slave_setup_on_AWS/files/12306792/Simplify-your-Puppet-Master-and-Puppet-slave-setup-on-AWS-with-these-straightforward-commands.pptx)


Congratulations! Your Puppet Master [Uploading Simplify-your-Puppet-Master-and-Puppet-slave-setup-on-AWS-with-these-straightforward-commands.pptx…]()
and Puppet Agent are now set up and running. You've tested the configuration to ensure everything is working smoothly.

Happy learning!

