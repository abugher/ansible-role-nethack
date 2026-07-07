# Install

    deploy-role-to-hosts nethack <hosts>

WARNING:  Old save files (and bones files, probably, if you keep those
locally) will be removed by the `make install` process.  You can set
them aside manually before an upgrade, at your discretion.

Add your user to the `games` group and to the `fuse` group if present.

# Configure

Write `~/.nethackrc` .  

# To Do

* Track bones file consumption among hosts and users.  
    * Currently, if a bones file is created for one user on one host, it will be added to that user's registry, and if it is consumed by that same user, it will be removed from the registry, but if it is consumed by a different user, the entry will remain forever in the first user's registry.  
    * Maybe a shared registry on the bones server with fields for user and host would solve this.  
    * Modern computers are big, text files are small, and humans are slow, so this bug should be very low impact.
* Track save files by version.
    * Probably the whole nethackdir can be version-specific.
    * This should probably be part of the build phase where hints get configured.
* Stop `make install` from clobbering save files.
    * Only implement this after successfully tracking save files by version, or version mismatch between save file and program will break things.
    * Before install, check the nethackdir for any save files and set them aside.
    * After install, restore any set aside save files.
