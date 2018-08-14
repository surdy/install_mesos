# A script to setup a Mesos cluster
## Introduction
This is a script that helps you set up a Mesos/Marathon cluster using the packages provided in the [Mesosphere](https://mesosphere.com/) repository. This script is based on the steps outlined [here](https://open.mesosphere.com/getting-started/install/).

The (install_mesos)[install_mesos] script does the following : 
* Detects the distro you are running
* Sets up the appropriate Mesosphere repo for your distro
* Installs Mesos and Marathon (including depencencies)
* Configures and restarts :
   * Mesos master/agent
   * Marathon
   * Zookeeper

This script currently only supports installation on the Mesosphere Supported distros: 

* Ubuntu 15.04 (vivid)
* Ubuntu 14.04 (trusty)
* Ubuntu 12.04 (precise)
* Debian 8 (jessie)
* Enterprise Linux 7 (RedHat/CentOS)
* Enterprise Linux 6 (RedHat/CentOS)

## Usage

```
Usage: install_mesos [--distro <distro>] [--masters <comma-separated-master-ip-list>] [--hostname <resolvable-hostname-for-node>] [--mesos <vesrion> [--marathon <version] <node-type>"

Examples:

install_mesos master

install_mesos agent

install_mesos master agent

install_mesos --masters \"1.1.1.1,2.2.2.2,3.3.3.3\" --hostname mesos-master-01 master

install_mesos --masters \"1.1.1.1,2.2.2.2,3.3.3.3\" --hostname mesos-master-01 --mesos 0.22.1 --marathon 0.8.2 master 
```

```
--distro
```
By default the script tries to detect the linux distro you are running on. But if you would like to bypass the detection specify the distro manually then you can use this option to specify the distro. This would be useful if the script is not detecting the distro correctly or if you are on a not so popular distro which is based on a popular distro e.g. Amazon linux 2015.09 is Redhat 6 based.

You can speficy the distro in this format: ubuntu-14.04, debian-8, rhel-6.5, centos-7 etc
```

--masters
```
Specify a comma separated list of IP addresses of all the masters in the cluster. This information is used to configure Mesos master service to find how many masters are there in the cluster and since we are setting up a cluster where mesos masters are co-located with the ZooKeeper instances we use the IP addresses to configure the ZooKeper URL(used in leader election). If this parameter is not specified it defaults to 1 master running on `localhost`.

```
--hostname
```
Specify the resolvable hostname of the node. If the hostname of the machine cannot be resolved directly (e.g., if on a different network or using a VPN), you may need to configure Mesos with a hostname value that you can resolve, for example, an externally accessible IP address or DNS hostname. This will ensure all links from the Mesos console work correctly. If this parameter is not specified Mesos uses system hostname and may lead to an internal hostname being used (As compared to an externally resolvable one)

```
--mesos
```
Specify the version of Mesos you would like to install. If you would like to install a specific version of Mesos you can use this parameter to specify that. By default it installs the latest version of Mesos.

```
--marathon
```
Specify the version of Marathon you would like to install. If you would like to install a specific version of Marathon you can use this parameter to specify that. By default it installs the latest version of Mesos.
