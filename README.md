# Install

  ./bin/deploy_role_to_hosts nethack <hosts>

WARNING:  Old save files (and bones files, probably, if you keep those
locally) will be removed by the 'make install' process.  You can set
them aside manually before an upgrade, at your discretion.

# Configure

Add your user to the ''games'' group and to the ''fuse'' group if
present.

# To Do

- Collision handling.  Before every move operation, check whether there
  is a same-named file.  Don't clobber it.  Look up whether bones files
  can be safely renamed.  Rename it and then rename it back later, if
  necessary.

- Cascading failures.  Might be necessary for above.
