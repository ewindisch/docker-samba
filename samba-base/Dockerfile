from ubuntu:latest

maintainer Eric Windisch <eric@windisch.us>

env DEBIAN_FRONTEND noninteractive

# Enable "extra" users, this makes
# overlaying our passwd/shadow/group content easier
run echo "deb http://archive.ubuntu.com/ubuntu precise main universe" >> /etc/apt/sources.list
run apt-get update
run apt-get install -y libnss-extrausers
run sed -i '/^\(passwd\|group\|shadow\):/{ s/$/ extrausers/; }' /etc/nsswitch.conf

# Install samba!
run apt-get install -y samba

# Add user management tool
add docker-smb-user /usr/local/bin/
