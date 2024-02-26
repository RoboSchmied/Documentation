# Things you should not do on linux terminal

Some times I do stupid things only to fix some other stupidities.
Here some examples of unpleasant moves:

## rename /lib64
```
sudo mv /lib64 /li64
```

As a result you can not execute a command anymore.
When rebooting you will end up in kernel panic.
Confirmed 'working' on Debian Bookworm.

### Fix:

Boot from another drive and rename the directory(link) back to /lib64.

```
sudo mv /li64 /lib64
```

 
## rm *
```
rm *
```
Using command history allot, I (as root) accidental ended up removing `*` in `/`.

### Prevention:

Do not use `rm *`.
Do not use `root` user whenever possible.
