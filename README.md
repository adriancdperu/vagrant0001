===========
Vagrant0001


Getting Started (per http://dev.classmethod.jp/server-side/server/fluentd-clustering/)
--------------------------------------------------------------------------------------
Server 1.

In your terminal:

    $ mkdir -p vagrant/server 1 && cd vagrant/server1
    $ vagrant box add server1 https://dl.dropbox.com/u/7225008/Vagrant/CentOS-6.3-x86_64-minimal.box
    $ vagrant init server1
    
Editing the Vagrant file:

    $ vim Vagrantfile
    config.vm.box = "server1"
    config.vm.network :private_network, ip: "192.168.33.10"
    
Vagrant up:

    $ vagrant up
    $ vagrant ssh

Noticed that the localhost is "localhost.localdomain"? Good.
Dont try anywhere than local. Get out the iptables provided by the kernel firewall so we
dont need to login as user root to perform stuff.

Japanese local time:

     $ cp -p /usr/share/zoneinfo/Japan /etc/localtime 

(if such a /usr/share/zoneinfo/Japan exists).

Install td-agent (https://github.com/treasure-data/td-agent). 
td-agent is an event collector daemon for Treasure Data, collecting various types of logs/events 
via various way, and transfer them to the cloud. td-agent is a distribution package of fluentd.

    $ sudo vi /etc/yum.repos.d/td.repo 
    [tresuredata]
    name=TreasureData
    baseurl=http://packages.treasure-data.com/redhat/$basearch
    gpgcheck=0
    $ sudo yum install -y td-agent

Got a message: Installed: td-agent.x86_64 0:1.1.13-0 
Complete!

Server 2.

Same as Server 1 in principle.

