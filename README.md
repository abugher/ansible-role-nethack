# Install

  ./bin/deploy_role_to_hosts nethack <hosts>

WARNING:  Old save files (and bones files, probably, if you keep those
locally) will be removed by the 'make install' process.  You can set
them aside manually before an upgrade, at your discretion.

# Configure

Add your user to the ''games'' group and to the ''fuse'' group if
present.

# To Do

* Handle multiple bones files of the same level.  This will require renaming
  each bones file to a unique name for shared storage, renaming it back to its
  canonical name for gameplay, and maintaining a map between those names.

* Review bones compatibility among recent versions of nethack.

* Abstract redundant code.  Start with a "register" function.
