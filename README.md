# Install

    deploy-role-to-hosts nethack <hosts>

WARNING:  Old save and bones files will be preserved.  The default behavior is
to delete old files, and this role contains significant efforts to subvert that
behavior.  While a major or minor upgrade will ignore old files, a patch
upgrade will continue to use old files.  (If you upgrade from 3.6.6 to 3.6.7,
your save file will still be in use.  If you upgrade from 3.6.7 to 5.0.0, your
old save will still exist, but it will be ignored.)  This may prevent the pain
of a deleted save file, but old files may contain incompatibilities or buggy
data.

Add your user to the `games` group and to the `fuse` group if present.

# Configure

Write `~/.nethackrc` .  

# To Do

* Track bones file consumption among hosts and users.  
    * Currently, if a bones file is created for one user on one host, it will be added to that user's registry, and if it is consumed by that same user, it will be removed from the registry, but if it is consumed by a different user, the entry will remain forever in the first user's registry.  
    * Maybe a shared registry on the bones server with fields for user and host would solve this.  
    * Modern computers are big, text files are small, and humans are slow, so this bug should be very low impact.
* Create version specific executables.
    * The launch script should take a version argument and launch the appropriate executable.
    * Old saves and bones could still be used this way, even after a newer version is installed.
