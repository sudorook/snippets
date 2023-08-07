# Samba

## Correct for mangled names

### Option 1

Add to the smb.conf:

```text
[global]
catia:mappings = 0x22:0xa8,0x2a:0xa4,0x2f:0xf8,0x3a:0xf7,0x3c:0xab,0x3e:0xbb,0x3f:0xbf,0x5c:0xff,0x7c:0xa6

[share name]
vfs objects = catia
```

Note the mappings are set up so that invalid characters can be mapped _to_ and
_from_ the same file on the server and client.

### Option 2

Add to the smb.conf:

```text
[share name]
vfs objects = catia fruit
fruit:encoding = native
```

## Make file names case-sensitive

Add to the smb.conf:

```text
[global]
case sensitive = yes
```

## Disable printers

Add to the smb.conf:

```text
load printers = no
printing = bsd
printcap name = /dev/null
disable spoolss = yes
show add printer wizard = no
```

## Print the full Samba configuration

To print the entire config, including all the default settings, run from the
terminal:

```text
testparm -vs
```
