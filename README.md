# Install

    deploy-role-to-hosts nethack <hosts>

WARNING:  Old save files (and bones files, probably, if you keep those
locally) will be removed by the `make install` process.  You can set
them aside manually before an upgrade, at your discretion.

Add your user to the `games` group and to the `fuse` group if present.

# Configure

Write `~/.nethackrc` .  

# To Do

* Track bones file consumption among hosts and users.  Currently, if a bones file is created for one user on one host, it will be added to that user's registry, and if it is consumed by that same user, it will be removed from the registry, but if it is consumed by a different user, the entry will remain forever in the first user's registry.  Maybe a shared registry on the bones server with fields for user and host would solve this.  Modern computers are big, text files are small, and humans are slow, so this bug should be very low impact.
