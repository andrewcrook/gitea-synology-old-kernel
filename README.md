# gitea-synology-old-kernel
Gitea 1.26.2 Docker has a compatibility issue with git expecting a newer kernel sys-calls. Synology are notorious for using old kernels. 


```console
500 Internal Server Error
An error occurred:

CreatePost, updateGitRepoAfterCreate: CreateRepository(git update-server-info): exit status 1 - error: unable to get random bytes for temporary file: Function not implemented
error: unable to update info/refs: Function not implemented
error: unable to get random bytes for temporary file: Function not implemented
error: unable to update objects/info/packs: Function not implemented
Gitea Version: 1.26.2
```

```console
# git update-server-info
error: unable to get random bytes for temporary file: Function not implemented
error: unable to update .git/info/refs: Function not implemented
error: unable to get random bytes for temporary file: Function not implemented
error: unable to update .git/objects/info/packs: Function not implemented
```

```console
#  strace -f git update-server-info | grep -i getrandom 
..
..
getrandom(0x7ffdab7955c0, 8, 0)         = -1 ENOSYS (Function not implemented)
write(2, "error: unable to get random byte"..., 79error: unable to get random bytes for temporary file: Function not implemented
) = 79
..
..
```
