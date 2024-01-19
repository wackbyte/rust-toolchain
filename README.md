# Install Rust Toolchain

This GitHub Action installs a Rust toolchain using rustup. It is designed to be
easy to use with good defaults.

It is a fork of [dtolnay/rust-toolchain] with a greater focus on stability\* and
ease of use at the cost of one-line usage. It also intends to expressly support
Gitea and Forgejo Actions.

\*The project is currently in an unstable development phase and will remain so
until the first version releases.

[dtolnay/rust-toolchain]: https://github.com/dtolnay/rust-toolchain

## Available remotes

This repository is mirrored on a few different remotes:

- [Codeberg] (Primary)
- [GitHub] (Secondary)

Please only submit issues and pull requests on Codeberg.

[Codeberg]: https://codeberg.org/wackbyte/rust-toolchain
[GitHub]: https://github.com/wackbyte/rust-toolchain

## Example workflow

```yaml
name: Rust
on:
  push:
  pull_request:

jobs:
  test:
    name: Test
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
  <th>Default value</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>toolchain</code></td>
  <td>(required)</td>
  <td>rustup toolchain name e.g. <code>stable</code>, <code>nightly</code>, <code>1.42.0</code>, <code>nightly-2022-01-01</code>&mdash;see <a href="https://rust-lang.github.io/rustup/concepts/toolchains.html#toolchain-specification" target="_blank">the documentation</a>. <strong>Consider putting the value between quotes to avoid it being parsed as a floating-point number.</strong></td>
</tr>
<tr>
  <td><code>targets</code></td>
  <td><code>''</code></td>
  <td>Comma-separated list of target triples to be additionally installed for this toolchain e.g. <code>wasm32-unknown-unknown</code>.</td>
</tr>
<tr>
  <td><code>components</code></td>
  <td><code>''</code></td>
  <td>Comma-separated list of components to be additionally installed for this toolchain e.g. <code>clippy, rustfmt</code>.</td>
</tr>
<tr>
  <td><code>profile</code></td>
  <td><code>'minimal'</code></td>
  <td>Group of components to install for this toolchain e.g. <code>minimal</code>, <code>default</code>, <code>complete</code>. Additional components can be installed with <code>components</code>.</td>
</tr>
<tr>
  <td><code>default</code></td>
  <td><code>false</code></td>
  <td>Set this toolchain as default. Equivalent to running <code>rustup default ${{steps.toolchain.outputs.name}}</code>.</td>
</tr>
<tr>
  <td><code>override</code></td>
  <td><code>false</code></td>
  <td>Set this toolchain as an override for this directory. Equivalent to running <code>rustup override set ${{steps.toolchain.outputs.name}}</code>. This is helpful if a <code>rustup-toolchain.toml</code> or <code>rustup-toolchain</code> file is present in the directory and you would like to use this toolchain instead.</td>
</tr>
</table>

## Outputs

<table>
<tr>
  <th>Name</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>cachekey</code></td>
  <td>A short hash of the installed rustc version e.g. <code>20220627a831</code>. Appropriate for use as a cache key.</td>
</tr>
<tr>
  <td><code>name</code></td>
  <td>rustup's name for the selected version of the toolchain e.g. <code>1.62.0</code>. Suitable for use with <code>cargo +${{steps.toolchain.outputs.name}}</code>.</td>
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
