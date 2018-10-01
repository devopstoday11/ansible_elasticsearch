# Ansible : Playbook Elasticsearch

The aim of this project is to deploy an Elasticsearch cluster on Vagrant.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

What things you need to run this Ansible playbook :

* [Vagrant](https://www.vagrantup.com/docs/installation/) must be installed on your computer
* Update the Vagrant file based on your computer (CPU, memory), if needed
* You must have download the ubuntu Xenial64 vagrant box :

```bash
$ vagrant box add https://app.vagrantup.com/ubuntu/boxes/xenial64
```

### Usage

A good point with Vagrant is that you can create, update and destroy all architecture easily with some commands.

Be aware that you need to be in the Vagrant directory to be able to run the commands.

#### Build Environment

Vagrant needs to init the project to run and build it :

```bash
$ vagrant up
```

After build, you can check which virtual machine Vagrant has created :

```bash
$ vagrant status
```

If everything run as expected, you should see something like this :

```bash
$ vagrant status

Current machine states:

elasticsearch01                  running (virtualbox)
elasticsearch02                  running (virtualbox)
elasticsearch03                  running (virtualbox)
```

#### Deployment

This playbook has some dependencies to other roles that must be downloaded before executing the playbook :

```bash
$ ansible-galaxy install -r requirements.yml
```

This command should download the Java role from Wikitops Github account to the local role path.

To deploy the Elasticsearch cluster, you just have to run the Ansible playbook elasticsearch.yml with this command :

```bash
$ ansible-playbook elasticsearch.yml
```

If everything run has expected, you should get the cluster status by this URL : http://10.0.3.121:9200/_cluster/health

Or by this curl command :

```bash
$ curl "http://10.0.3.121:9200/_cluster/health?pretty"
{
  "cluster_name" : "ELS_DEFAULT_NAME",
  "status" : "green",
  "timed_out" : false,
  "number_of_nodes" : 3,
  "number_of_data_nodes" : 3,
  "active_primary_shards" : 0,
  "active_shards" : 0,
  "relocating_shards" : 0,
  "initializing_shards" : 0,
  "unassigned_shards" : 0,
  "delayed_unassigned_shards" : 0,
  "number_of_pending_tasks" : 0,
  "number_of_in_flight_fetch" : 0,
  "task_max_waiting_in_queue_millis" : 0,
  "active_shards_percent_as_number" : 100.0
}
```

#### Destroy

To destroy on what Vagrant has created, just run this command :

```bash
$ vagrant destroy
```

## Author

Member of Wikitops : https://www.wikitops.io/

## Licence

This project is licensed under the Apache License, Version 2.0. For the full text of the license, see the LICENSE file.
