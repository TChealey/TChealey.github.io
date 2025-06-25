# Secure SSH Configuration (Hardening SSH Access)

This guide documents the steps I took to harden SSH access on a Linux system formy personal security project.

## Objective

To reduce security risks associated with remote access by:
- Changing the default SSH port
- Disabling root login
- Disabling password-based authentication
- Confirming the SSH service is running securely

## Steps Taken

Opened the SSH daemon config file using 'vim':

'''bash
sudo vim /etc/ssh/sshd_config

## Made the following changes inside the file:
Port 2223
PermitRootLogin no
PasswordAuthentication no
AddressFamily any
ListenAddress 0.0.0.0
Note: I choose port 2223 instead of the default 22 to reduce bot attacks on SSH

## Updated SELinux to allow the new SSH port:

sudo semange port -a -t ssh_port_t -p tcp 2223

## Opened the new port in the firewall:

sudo firewall-cmd --add-port=2223/tcp --permanent
sudo firewall-cmd --reload

## Reloaded the SSH daemon and restarted the service:

sudo systemctl daemon-reexec
sudo systemctl restart sshd

## Verified that SSH is listening on the new port:

sudo ss -tuln | grep 2223

## Result

The SSH service is now active and listening on port 2223. Root login and password autentication have been disabled. SSH is secured for remote connections.
