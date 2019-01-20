# SSH

## Generate a new SSH key

```
ssh-keygen -t rsa -b 4096 -o -a 100 -f ~/.ssh/<id>_rsa -q -N ""
```

Note: The -o flag specifies that the key be saved in the new OpenSSH key format
(v6.5, 2014), which is incompatible with older versions.


## Use SSH key to login to remote server

```
ssh-copy-id -i <identity> <user>@<server>
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

### Make the SSH master connection persist after closing

Add the additional line to the ~/.ssh/config:

```
Host <hostname>
  ControlMaster auto
  ControlPath ~/.ssh/cm_socket/%r@%h:%p
  ControlPersist yes
```

This will make the SSH connection persist after closing the connection. Instead
of `yes`, you can specify a time limit (e.g. 1h) so that the connection closes
eventually.

To manually kill the background connection, run:
```
ssh -O exit <user>@<server>
```
