# Links
- https://puppet.com/docs/bolt/latest/getting_started_with_bolt.html
- https://puppet.com/docs/bolt/latest/running_bolt_commands.html
- https://puppet.com/docs/bolt/latest/projects.html

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
