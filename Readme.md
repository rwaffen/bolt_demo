# Links
- https://puppet.com/docs/bolt/latest/getting_started_with_bolt.html
- https://puppet.com/docs/bolt/latest/running_bolt_commands.html
- https://puppet.com/docs/bolt/latest/projects.html

# Getting Started fast
    mkdir my_project
    cd my_project
    bolt project init my_project
    mkdir -p modules/apache/plans
    mkdir -p modules/apache/files

    touch Dockerfile
    # add content from dockerfile

    touch docker-compose.yaml
    # add content from compose file

    docker-compose up -d --build
    docker-compose ps

    bolt command run whoami -t 127.0.0.1:2000 -u root -p root --no-host-key-check

    touch inventory.yaml
    # add content from inventory

    bolt command run whoami -t target1

    touch modules/apache/plans/install.yaml
    # add content from install.yaml

    bolt plan run apache::install -t containers

    curl 127.0.0.1:3000

    touch modules/apache/files/start_apache.sh
    # add content from apache.sh

    bolt plan run apache::install -t containers

    touch modules/apache/files/index.html
    # add content from index.html

    bolt plan run apache::install -t containers src=apache/index.html

    curl 127.0.0.1:3000

# additional bolt commands
    bolt command run 'pwd' --targets containers
    bolt command run @modules/apache/files/configure.sh --targets containers
    cat modules/apache/files/configure.sh | bolt command run - --targets containers

    bolt command run 'pwd' --targets target1
    bolt command run 'pwd' --targets 'target*'
    bolt command run 'pwd' --targets '@targets.txt'
    cat targets.txt | bolt command run 'pwd' --targets -


    bolt script run ./modules/apache/files/configure.sh --targets containers

    bolt task run facts --targets containers

    bolt task run package action=status name=apache2 --targets containers
    bolt task run package action=status name=puppet-agent --targets containers

    bolt task run reboot --targets containers

    bolt file upload ./modules/apache/files/configure.sh /tmp/configure.sh --targets containers
    bolt file download /tmp/configure.sh ./modules/apache/files/configure2.sh --targets containers

    # also installs puppet
    bolt apply manifests/servers.pp --targets containers
    bolt task run package action=status name=puppet-agent --targets containers

    bolt apply --execute "file { '/etc/puppetlabs': ensure => present }" --targets containers

    # targets over puppetdb

    # repo meta update
    bolt --query "inventory[certname] { facts.osfamily = 'RedHat' and facts.puppetversion ~ '^5.*' }" command run -c5 "sudo yum clean all"

    # update puppet agent
    bolt --query "inventory[certname] { facts.osfamily = 'Redhat' and facts.puppetversion ~ '^5.*' }" task run -c 5 --run-as root package name=puppet-agent action=upgrade
