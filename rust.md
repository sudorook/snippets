# Rust

## Use crates from Debian repositories

To exclusively use crates packaged by Debian and avoid entirely the use of
`crates.io`, create a `${HOME}/.cargo/config.toml` file and add:
```toml
[net]
offline = true

[source]

[source.crates-io]
replace-with = "debian"

[source.debian]
directory = "/usr/share/cargo/registry"
```

**Note:** Should you run into checksum errors, remove the package `Cargo.toml`
file. It contains checksums for packages, and those for the Debian packages in
`/usr/share/cargo/registry` will not match those from `crates.io`.
