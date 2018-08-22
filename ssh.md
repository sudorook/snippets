# SSH

## Generate a new SSH key

```
ssh-keygen -t rsa -b 4096 -o -a 100 -f ~/.ssh/<id>_rsa -q -N ""
```

Note: The -o flag specifies that the key be saved in the new OpenSSH key format
(v6.5, 2014), which is incompatible with older versions.


## Use SSH key to login to remote server

```
ssh-copy-id -i <identity> <user@server>
```
