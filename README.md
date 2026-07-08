# Goals

This role installs nethack, but it also applies a number of very specific
preferences and customizations.

## Build Nethack

When deployed to a target host, this role will install the source code for
nethack, apply some customization, and compile nethack.

## Customize Nethack

Check the build script for specifics.  Generally, the compiled nethack will
refer to a version-specific nethackdir for save and bones files, and a few
non-default run-time settings will be created.

## Install Nethack

Once the game is built, `make install` does the installation.  This role
overrides some default behavior.

### Preserve Old Saves and Bones

Old save and bones files will be preserved.  The default behavior is to delete
old files, and this role contains significant efforts to subvert that behavior.
While a major or minor upgrade will ignore old files, a patch upgrade will
continue to use old files.  (If you upgrade from 3.6.6 to 3.6.7, your save file
will still be in use.  If you upgrade from 3.6.7 to 5.0.0, your old save will
still exist, but it will be ignored.)  

WARNING:  This may prevent the pain of a deleted save file, but old files may
contain incompatibilities or buggy data.

### Preserve Old Nethack Versions

WARNING:  This behavior was introduced around the release of nethack 5.0.0.
Earlier versions installed by this role will not benefit from this feature, and
will probably become unplayable when the role is redeployed.

The `nethack` executable file installed by this role will be immediately
renamed with the full version number.  A symlink to that versioned executable
will be put in place of the executable.  Future deployments of different
versions should create new versioned executables and replace the symlink.  Old
versioned executables should be left in place.

An old version of nethack can be played, complete with any old save and bones
files, by specifying the full version number:

    /usr/local/bin/nethack 5.0.0

Without that argument, the most recently installed version of nethack will be
launched.

## Install Wrapper

A wrapper script will be installed at `/usr/local/bin/nethack`.  

### Bones Exchange

A major purpose of the script is to automatically exchange bones files with a
central server.  A few bones will be downloaded before launching the game, if
any bones are available, and after the game any remaining or new bones will be
uploaded.  Download and upload are move operations, not copy, so once a bones
file is consumed, it is gone, as is traditional.

Bones files are kept in version specific locations on the server, similar to
save and bones files kept locally.  Versions of the game with the same major
and minor version, even with different patch version, will share bones files.

WARNING:  Sharing across patch versions may go against the advice of release
notes.  It will probably be fine, but if the game breaks on a bones file, this
might be why.

# Usage

How to use this role depends somewhat on what addition is being made.  There
could be a new host, a new user account, a new player, or some combination.

## New Host

There is a new host where nethack should be available.

### Inventory

Add the target host to the `nethack` group.  

    [nethack]
    targethost

Define at least one user as a nethack player in the host vars.  

    nethack_users:
      - 'targetuser'

Make sure a public key key for that user at that host is available to ansible.

### Deployment

Deploy role `cryptkeeper`.  That will update the server for bones exchange,
allowing the new user at the new host to participate.

    deploy-role cryptkeeper

Deploy role `nethack` to make the game and wrapper available on the target
host.

    deploy-role nethack

## New User

Nethack should be made available to a new user account on a host where some
user accounts already have access.

Refer to the [New Host](#new-host) instructions.  The target host may already
be a member of the `nethack` role, but the rest of the instructions are
necessary and sufficient to enable a new user.

## New Player

There is a person who has not played nethack before.

Refer to the [New Host](#new-host) instructions, to start.  

Make sure the person knows to start `/usr/local/bin/nethack`, or has a PATH
such that just `nethack` will execute that file.

Learning to play nethack is somewhat out of scope for this role.  Recommended
first steps:

* Launch the game, and accept the invitation to play a tutorial.
* Check the in-game help, starting by typing '?'.
* With the warning of spoilers, refer heavily to [the wiki](https://nethackwiki.com).
* Write `~/.nethackrc` .  
    * [reference](https://nethackwiki.com/wiki/Options)
    * [example](https://github.com/abugher/home/blob/master/.nethackrc)
    * Leave `legacy` enabled (default) until tired of seeing the "go bravely" text at every game start.
* Review terminal colors.
    * Make sure you can tell all the colors apart from each other.
    * Make sure all colors are visible on the background color.
    * Watch out for dark blue, light blue, and cyan, in particular.
    * This role installs some X11 configuration for that purpose, used mainly by xterm.
    * Other terminal emulators may expose color configuration in the settings menu.

# To Do

* Track bones file consumption among hosts and users.  
    * Currently, if a bones file is created for one user on one host, it will be added to that user's registry, and if it is consumed by that same user, it will be removed from the registry, but if it is consumed by a different user, the entry will remain forever in the first user's registry.  
    * Maybe a shared registry on the bones server with fields for user and host would solve this.  
    * Modern computers are big, text files are small, and humans are slow, so this bug should be very low impact.
