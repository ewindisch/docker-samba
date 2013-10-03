Samba for Docker
================

This runs a basic samba server underneath docker with a
number of limitations and constraints.

This supports a tdb backend and unix users. Unix
users are managed via a dedicated set of files for
passwd/shadow/group.

Configuring
===========

These Docker containers must be configured so that
you may have users and working shares.

Share Paths (Docker)
--------------------

It is necessary to tell Docker which directories on the host may
be shared into the container. If these directories were not visible
to the container, Samba would be unable to expose these shares to
the network.

Edit etc/defaults/docker to set your share paths:

    SHARE_DIR=/path/to/files/all/users/can/see
    GUEST_DIR=/path/to/files/all/guests/can/see
    HOME_DIR=/home

These will all be bind-mounted to the samba-smbd container,
there is presently no way to disable any of these mounts. To disable
a share path, point it to an empty directory, edit smb.conf,
or edit launch.sh; Ideally, edit smb.conf and launch.sh both.

Samba Shares & Configuration
----------------------------

The default samba configuration should serve for very basic
needs within the constraints of what is possible and reasonable
within a Docker environment.

Still, it is likely that you'll want to change the configuration.

Edit etc/smb/smb.conf as desired and relaunch your containers.

Users
-----

User management is performed through tdb and standard
Unix password/shadow files. Edit these files within the
etc/ directory and relaunch your containers.

For convenience, a user management tool is available as:

    $ ./samba-docker usermod [add|delete|password] <user> <password>

The password option is mandatory for 'add' and 'password'. If
supplied, the password is ignored for the 'delete' feature.

Running
=======

    $ ./samba-docker build
    $ ./samba-docker launch

The build process should only need to be performed once, unless
code changes have been made or an upgrade is being performed.

These commands *MUST* be run as root, or with a user granted
priviledges to build and launch docker containers.
