# pgsql-backup

This is a bash program that uses pg_dumpall and pg_dump to back up all roles, tablespaces, and databases of a PostgreSQL cluster, either local or remote. It has been in continuous use on many servers since the earliest simpler versions dating to around the year 2002.

Each database is exported into its own file in plain text format for archival and cross-version accesibility.

The database file is then compressed using one of the common compression tools, currently zstd, xz, pxz, lbzip2, pbzip2, bzip2, pigz, or gzip.

The compression can be done inline if desired to reduce disk space required, or of an intermediate uncompressed pg_dump output file on disk so that parallel compression threads can be used.

Each new export file is deleted if it is identical to the previous one so that the timestamp and inode will not change, to minimize changes visible to backup tools such as rsync.

Configuration allows optionally excluding some databases, and dumping databases in order of either size or name.
