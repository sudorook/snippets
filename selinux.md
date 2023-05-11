# SELinux

## Address `Regex version mismatch` errors

This issue may be caused by package upgrades causing version mismatches with
the existing SELinux policy. To suppress these messages, rebuild using the
existing packages.

Be sure, first, that upgrades or some other innocent issue is actually causing
the policy version mismatches.

As root, run:
```sh
semodule -B
```
