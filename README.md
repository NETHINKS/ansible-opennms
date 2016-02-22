#  Ansible Playbooks for Installing OpenNMS
This is an Ansible Playbook for installing the OpenSource Network Management System OpenNMS:

The following steps are executed:
- Upgrade the system using the packet management
- Install and configure snmpd using the packet management
- Install a cronjob for time sync with ntpdate
- Install PostgreSQL server with local access
- Install Oracle Java JDK
- Install Jicmp
- Install OpenNMS and register as initd/systemd service

## Available Playbooks
There are two playbooks for installing OpenNMS:

opennms-install-packaging.yml will install OpenNMS using the paket management system (e.g. apt/yum) of the linux distribution. A internet connection is required on the target machine, as the packages will be downloaded from opennms.org. This is supported on Debian and RedHat based distributions.

opennms-install-archive.yml will install OpenNMS using archive files of OpenNMS, Oracle Java JDK and ICMP that needs to be placed in the "repository" directory of the playbook. This is supported on Debian, RedHat and SuSE based distributions.

## Usage of opennms-install-archive.yml
This playbook will install OpenNMS using archive files for the required software.
If you want to use this playbook, you need to download the following software. Place it in the "repository" directory:
- Jicmp4 (as .tar.gz)
- Jicmp6 (as .tar.gz)
- Oracle Java JDK (as .tar.gz)
- OpenNMS (as .tar.gz / see http://www.opennms.org/wiki/Installation:Source for creating)

Software like ntpdate, snmpd and PostgreSQL will be installed using the packet management of your distribution.

For adhoc executing the playbook on a remote machine with login and password:
```
ansible-playbook -i <Host>, -k opennms-install-archive.yml 
ansible-playbook -i 192.168.0.11, -k opennms-install-archive.yml 
```
For adhoc executing the playbook on the local machine:
```
ansible-playbook -i localhost, -c local opennms-install-archive.yml 
```

After starting, the user will be asked to set a few variables:
<table>
<tr><td>jicmp archive file</td><td>Place on the local machine, where the jicmp tar.gz archive is stored</td></tr>
<tr><td>jicmp6 archive file</td><td>Place on the local machine, where the jicmp6 tar.gz archive is stored</td></tr>
<tr><td>Oracle Java JDK archive file</td><td>Place on the local machine, where the Oracle Java tar.gz archive is stored</td></tr>
<tr><td>OpenNMS archive file</td><td>Place on the local machine, where the OpenNMS tar.gz archive is stored</td></tr>
<tr><td>path for installing</td><td>Path on the remote machine, where the software should be installed</td></tr>
<tr><td>NTP: set NTP server</td><td>NTP server for time synchronization</td></tr>
<tr><td>SNMP: set community</td><td>SNMP community for snmpd</td></tr>
<tr><td>SNMP: set SysLocation</td><td>SNMP SysLocation value for snmpd</td></tr>
<tr><td>SNMP: set SysContact</td><td>SNMP SysContact value for snmpd</td></tr>
</table> 

Supported are the follwing operating systems:
- Debian (e.g. Debian, Ubuntu)
- RedHat (e.g. RedHat, Oracle Linux, CentOS)
- Suse (e.g. SuSe Linux Enterprise, openSUSE, openSUSE Leap)

With Suse, automatic updates are not supported at the moment


## Usage of opennms-install-packaging.yml
This will install OpenNMS using the packet management (apt/yum) of your distribution. An Internet connection on the target machine is required for using this playbook.

For adhoc executing the playbook on a remote machine with login and password:
```
ansible-playbook -i <Host>, -k opennms-install-packaging.yml 
ansible-playbook -i 192.168.0.11, -k opennms-install-packaging.yml 
```
For adhoc executing the playbook on the local machine:
```
ansible-playbook -i localhost, -c local opennms-install-packaging.yml 
```

After starting, the user will be asked to set a few variables:
<table>
<tr><td>NTP: set NTP server</td><td>NTP server for time synchronization</td></tr>
<tr><td>SNMP: set community</td><td>SNMP community for snmpd</td></tr>
<tr><td>SNMP: set SysLocation</td><td>SNMP SysLocation value for snmpd</td></tr>
<tr><td>SNMP: set SysContact</td><td>SNMP SysContact value for snmpd</td></tr>
</table> 

Supported are the follwing operating systems:
- Debian (e.g. Debian, Ubuntu)
- RedHat (e.g. RedHat, Oracle Linux, CentOS)


## Requirements
- Ansible 2.0 or higher
