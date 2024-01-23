# Install Rust Toolchain

This Action installs a Rust toolchain using rustup. It is designed to be easy to
use with good defaults.

## Project information

This project is a fork of [dtolnay/rust-toolchain] with a greater focus on
stability and ease of use at the cost of one-line usage. It intends to expressly
support all of GitHub, Gitea, and Forgejo Actions.

[dtolnay/rust-toolchain]: https://github.com/dtolnay/rust-toolchain

### Available mirrors

This repository is mirrored on a few different remotes:

- [Codeberg] (Primary)
- [GitHub] (Secondary)

Please only submit issues and pull requests on Codeberg.

[Codeberg]: https://codeberg.org/wackbyte/rust-toolchain
[GitHub]: https://github.com/wackbyte/rust-toolchain

## Example workflow

```yaml
name: CI
on:
  push:
  pull_request:

jobs:
  test:
    name: cargo test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: wackbyte/rust-toolchain@trunk
        with:
          toolchain: stable

      - run: cargo test --all-features
```

## Inputs

<table>
<tr>
  <th>Name</th>
  <th>Description</th>
  <th>Default value</th>
</tr>
<tr>
  <td><code>toolchain</code></td>
  <td>

  rustup toolchain name.
  It is recommended to use quotes in order to avoid versions being parsed as floating-point numbers.

  Example values:
  - `stable`
  - `nightly`
  - `1.42.0`
  - `nightly-2022-01-01`

  ([documentation][toolchain-doc])
  </td>
  <td>(required)</td>
</tr>
<tr>
  <td><code>targets</code></td>
  <td>

  Comma-separated list of target triples to be additionally installed for this toolchain.

  Example value: `wasm32-unknown-unknown`

  ([documentation][targets-doc])
  </td>
  <td>(empty)</td>
</tr>
<tr>
  <td><code>components</code></td>
  <td>
  
  Comma-separated list of components to be additionally installed for this toolchain.

  Example value: `clippy, rustfmt`

  ([documentation][components-doc])
  </td>
  <td>(empty)</td>
</tr>
<tr>
  <td><code>profile</code></td>
  <td>
  
  Group of components to install for this toolchain.

  Available values:
  - `minimal`
  - `default`
  - `complete`

  ([documentation][profile-doc])
  </td>
  <td><code>minimal</code></td>
</tr>
<tr>
  <td><code>default</code></td>
  <td>

  Set this toolchain as default.
  Equivalent to running `rustup default` with this toolchain.

  ([documentation][default-doc])
  </td>
  <td><code>false</code></td>
</tr>
<tr>
  <td><code>override</code></td>
  <td>

  Set this toolchain as an override for this directory.
  Equivalent to running `rustup override set` with this toolchain.
  This is helpful if a `rustup-toolchain.toml` or `rustup-toolchain` file is present in the directory and you would like to use this toolchain instead.

  ([documentation][override-doc])
  </td>
  <td><code>false</code></td>
</tr>
</table>

[toolchain-doc]: https://rust-lang.github.io/rustup/concepts/toolchains.html#toolchain-specification
[targets-doc]: https://doc.rust-lang.org/rustc/platform-support.html
[components-doc]: https://rust-lang.github.io/rustup/concepts/components.html
[profile-doc]: https://rust-lang.github.io/rustup/concepts/profiles.html
[default-doc]: https://rust-lang.github.io/rustup/overrides.html#default-toolchain
[override-doc]: https://rust-lang.github.io/rustup/overrides.html

## Outputs

<table>
<tr>
  <th>Name</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>cachekey</code></td>
  <td>

  A short hash of the installed rustc version.
  Appropriate for use as a cache key.

  Example value: `20220627a831`
  </td>
</tr>
<tr>
  <td><code>name</code></td>
  <td>

  rustup's name for the selected version of the toolchain.
  Suitable for use with the `cargo +toolchain` shorthand.

  Example value: `1.62.0`
  </td>
</tr>
</table>

## Toolchain expressions

The following forms are available for projects that use a sliding window of
compiler support.

```yaml
# Installs the most recent stable toolchain as of the specified time offset,
# which may be written in years, months, weeks, or days.
- uses: wackbyte/rust-toolchain@trunk
  with:
    toolchain: stable 18 months ago
```

```yaml
# Installs the stable toolchain which preceded the most recent one by the
# specified number of minor versions.
- uses: wackbyte/rust-toolchain@trunk
  with:
    toolchain: stable minus 8 releases
```

## License

The scripts and documentation in this project are released under the [MIT
License].

[MIT License]: LICENSE
