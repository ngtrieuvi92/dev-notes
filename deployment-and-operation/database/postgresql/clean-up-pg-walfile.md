# Clean up pg walfile

```
SELECT pg_walfile_name(pg_current_wal_lsn())
```

```
pg_archivecleanup  /var/lib/postgresql/archive 000000010000000C00000021
```

