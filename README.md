# vagrant-cassandra-cluster

## Requirements

- Vagrant
- Ansible > 1.3
- [The Ansibles](https://github.com/pjan/the-ansibles) roles


## Instructions

It is pre-configured to set up 3 cassandra nodes (vagrant boxes) in a single rack configuration. To set-up a different configuration, change the `vagrantfile`, the `hosts` file in the data directory, the `cassandracluster` file and the `host_vars` files in the ansible folder. You can use the `tokengentool` script (`./tokengentool`) to generate the correct tokens.

Now:

1. add your public ssh key into `group_vars/all` so you can ssh passwordless in each of the boxes, and optionally change the cluster name.

2. `vagrant up` in the `Vagrantfile` directory

3. Clone the `The Ansibles` repo, and move the contents of the `ansible` repo into that repo's root. Change directory into the repo's root, and run the ansible playbook.

```
ansible-playbook -i cassandracluster cassandracluster.yml -u vagrant -k --sudo
```

and enter `vagrant` in the password prompt.

**Hammertime!**
