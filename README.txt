WARNING:  Old save files (and bones files, probably, if you keep those
locally) will be removed by the 'make install' process.  You can set
them aside manually before an upgrade, at your discretion.

TODO:

- Concurrency handling.  If more than one nethack instance happens on
  the same system, they shouldn't upload each other's bones files.
  (They might consume each others bones files, but that shouldn't look
  different from consuming their own.)  Lock every bones file against
  other instances uploading it.  When finished, upload all unlocked
  bones.  Clean up lock files for missing bones.

- Collision handling.  Before every move operation, check whether there
  is a same-named file.  Don't clobber it.  Look up whether bones files
  can be safely renamed.  Rename it and then rename it back later, if
  necessary.

- Failure handling.  If something goes wrong, especially if a lock
  or unlock fails, clean up all locks before bailing out if possible.

- Cascading failures.  Might be necessary for above.
