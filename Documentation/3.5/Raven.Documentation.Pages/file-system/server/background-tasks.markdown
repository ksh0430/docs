#Background tasks

#Renames and deletes

When a file is removed or renamed, the relevant configuration items are created in the file system: `DeleteOp/[FILENAME]` and `RenameOp/[FILENAME]`.
Basically, they are markers to indicate that an operation was initiated for a given file. The configuration will be deleted only if a related file operation finishes successfully.

Note that these actions performed on the large files can take a while. Based on the prefixed configuration items the file system is able to resume the file deletion or its rename if a server was restarted in the middle. There are two background tasks which detect if any operation needs to be retried. They run periodically, every 15 minutes.

#Synchronization

Another background work is the synchronization of the files to destination nodes. It is performed periodically to ensure that all the modifications are  propagated to the destinations, even though one of them was down for a long time. If a destination server wakes up, then our file system will resend all the missing file updates. The synchronization task is run every 10 minutes.


## Related articles

- [Commands : CleanUpAsync](../client-api/commands/storage/cleanup)
- [Commands : RetryRenamingAsync](../client-api/commands/storage/retry-renaming)
- [Commands : StartAsync](../client-api/commands/synchronization/start)