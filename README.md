#  Ansible Playbook for Installing OpenNMS
This is an Ansible Playbook for installing the OpenSource Network Management System OpenNMS:

The following steps are executed:
- Upgrade the system using the packet management
- Install and configure snmpd using the packet management
- Install a cronjob for time sync with ntpdate
- Install PostgreSQL server with local access
- Install Oracle Java JDK
- Compile and Install Jicmp
- Install OpenNMS and register as initd/systemd service

## Usage
If you want to use this playbook, you need to download the following software. Place it in the "repository" directory:
- Jicmp4 (as .tar.gz)
- Jicmp6 (as .tar.gz)
- Oracle Java JDK (as .tar.gz)
- OpenNMS (as .tar.gz)

For adhoc executing the playbook on a remote machine with login and password:
```
ansible-playbook -i <Host>, -k opennms-install.yml 
ansible-playbook -i 192.168.0.11, -k opennms-install.yml 
```
For adhoc executing the playbook on the local machine:
ansible-playbook -i localhost, -c local opennms-install.yml 

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

## Supported OS
The follwing ansible os families are supported:
- Debian (e.g. Debian, Ubuntu)
- RedHat (e.g. RedHat, Oracle Linux, CentOS)
- Suse (e.g. SuSe Linux Enterprise, openSUSE, openSUSE Leap)

With Suse, automatic updates are not supported at the moment

## Requirements
- Ansible 2.0 or higher
