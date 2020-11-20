# linux

### shell

### daemon

When a daemon starts up, it has to do some low-level housework to get itself ready for its real job

1. Fork off the parent process(init process with pid 0 is the new parent)
2. Change file mode mask (umask)
3. Open any logs for writing
4. Create a unique Session ID (SID)
5. Change the current working directory to a safe place
6. Close standard file descriptors
7. Enter actual daemon code