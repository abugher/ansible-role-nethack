WARNING:  Old save files (and bones files, probably, if you keep those
locally) will be removed by the 'make install' process.  You can set
them aside manually before an upgrade, at your discretion.

TODO:

- Failure handling.  If something goes wrong, especially if a lock
  or unlock fails, clean up all locks before bailing out if possible.

- Collision handling.  Before every move operation, check whether there
  is a same-named file.  Don't clobber it.  Look up whether bones files
  can be safely renamed.  Rename it and then rename it back later, if
  necessary.

- Cascading failures.  Might be necessary for above.
