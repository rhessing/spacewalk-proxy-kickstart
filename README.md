spacewalk-proxy-kickstart
=========================

Ability to Kickstart Servers Using Spacewalk Proxy Server (Spacewalk 2.1 / Spacewalk Proxy 2.1)

The scripts provided here should be put into /opt/swproxy-sync.

Please change all areas marked with < > brackets, these will need to be updated with your actual settings.

To get this to work:

On the Spacewalk Server:
1. edit /etc/cobbler/rsync.template add the following:

[spacewalk-tftp]
    path    = /var/lib/tftpboot
    comment = PXE TFTPBOOT Directory

2. edit /etc/cobbler/settings change
manage_rsync: 1

3. check /etc/xinet.d/rsync make sure disable is no. Restart xinetd if necessary

4. cobbler sync - will make live rsync changes.


On the proxy Server (centos in this case)

1. Install the following packages:
yum install yum-utils xinetd tftp-server createrepo rsync dhcp dhcp-common

2. edit /etc/xinet.d/tftp set disable to no and start/restart xinetd 

3. Clone this repo and put it on the spacewalk proxy server.

4. Make Sure iptables allows all necessary ports through.

5. Edit the templates/dhcp.template and edit the scripts make sure all of the settings are correct for your environment.

6. Then run proxy-dhcp followed by proxy-rsync

Try to build a server using the Proxy server - you should be prompted with the tftpboot menu from the Main Spacewalk server.
This is a very basic version, but enough to get the spacewalk proxy server capable of kickstarting.

Lock down all services as necessary once you have it working - feel free to improve the scripts - they are very basic used for a poc.

If you do improve the scripts / come up with better methods I would really appreciate it if you could share the updates back.

-Vamegh
