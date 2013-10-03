from ubuntu:latest

maintainer Eric Windisch <eric@windisch.us>

run apt-get install -y samba

expose 137:137/udp
expose 138:138/udp

entrypoint ["/usr/sbin/nmbd"]
cmd ["-F"]
