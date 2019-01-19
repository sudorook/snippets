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

## Use SSH multiplexing to avoid multiple authentications

Add the following to your ~/.ssh/config file:

```
Host <hostname>
  ControlMaster auto
  ControlPath ~/.ssh/cm_socket/%r@%h:%p
```

Create the ~/.ssh/cm_socket directory if it doesn't already exist.

You can also use a wildcard for the hostname to enable this for all domains.
