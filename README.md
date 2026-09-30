# filla-cakar - encrypted media mirror

Production customer media (access photos, premises videos), each file
encrypted individually with AES256 using the **same passphrase as the restic
repository** - your password manager, entry for the filla-cakar backup.

Layout mirrors the server: `media/customer_<id>/<uuid>.<ext>.gpg`.
`manifest.json` records the SHA-256 of each *plaintext* source file, which is
how the next run knows what changed.

Decrypt one file:

    gpg --decrypt media/customer_147/abc.mp4.gpg > abc.mp4

Decrypt everything:

    find media -name '*.gpg' -exec sh -c 'gpg --quiet --decrypt "$1" > "${1%.gpg}"' _ {} \;

Files are encrypted individually rather than as one archive on purpose: a
single archive would change in its entirety whenever one photo was added,
re-uploading everything on every run.

This is a SECOND copy and a stopgap. The full backup - both databases, the
code bundle, host config, and file history - is the restic repository. See
`scripts/backup/RESTORE.md` in the application repository.

Files: 167    Last updated: 2026-09-30 16:25:52 +10:00
