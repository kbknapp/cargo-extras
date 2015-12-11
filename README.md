# cargo-extras

Linux: [![Travis](https://img.shields.io/travis/kbknapp/cargo-extras.svg)](https://travis-ci.org/kbknapp/cargo-extras)

Latest on crates.io: [![Crates.io](https://img.shields.io/crates/v/cargo-extras.svg)](https://crates.io/crates/cargo-extras)

Latest on Github: [![GitHub release](https://img.shields.io/github/release/kbknapp/cargo-extras.svg)](https://github.com/kbknapp/cargo-extras/releases)

A collection of [cargo](https://github.com/rust-lang/cargo) subcommands for use while working on [Rust](https://www.rust-lang.org/) source code and projects. This repository and package aims to make it easy to install all the additional commands at once.

## Installing

You can install all of the subcommands included in `cargo-extras` with a single `cargo install`.

### Prerequisites

Because one of the subcommands requires `cmake` to build, you must have `cmake` installed on your system. Follow your operating system's guidance for installing this package.

### Primary Method: `cargo install`

To install from [crates.io](https://crates.io) simply run 

```
$ cargo install cargo-extras
```

Alternatively you can track the latest on the master branch in this repo (if the version badges above are different, the master branch here may contain bleeding edge updates that haven't been released to the crates.io version):

```
$ cargo install --git https://github.com/kbknapp/cargo-extras
```

To see all the commands that are now installed (to include standard `cargo` commands):

```
$ cargo --list
```

If you get an error about the `install` command not being found, or are using `multirust`<sup>[1](https://github.com/Diggsey/multirust-rs),[2](https://github.com/brson/multirust)</sup> you could run:

```
$ multirust run nightly cargo install cargo-extras
```

**Note:** As of Rust 1.5 the `cargo install` command is included, no more requirement to use a nightly compiler. So if you are receiving the above error, and using a stable compiler version, ensure that you have at least Rust 1.5

You may also, instead compile and install the traditional way by following the instructions below.

#### OSX Specific Issue

On El Capitan there is an issue with `openssl-sys` (see [the related issue](https://github.com/sfackler/rust-openssl/issues/255)) which can be solved by running these two commands (assuming you have [Homebrew](http://brew.sh))

```
$ brew install openssl
$ OPENSSL_INCLUDE_DIR=/usr/local/opt/openssl/include cargo install cargo-extras
```

### Alternate Method: Compiling

Follow these instructions to compile `cargo-extras`, then skip down to Installation.

 1. Ensure you have current version of `cargo` and [Rust](https://www.rust-lang.org) installed
 2. Clone the project `$ git clone --recursive https://github.com/kbknapp/cargo-extras && cd cargo-extras`
 3. Build the project `$ cargo build --release` (**NOTE:** There is a large performance difference when compiling without optimizations, so I recommend always using `--release` to enable to them)
 4. Once complete, all the binaries will be located at `target/release/`

#### Installation 

All you need to do is place the binary subcommands somewhere in your `$PATH`. Then run `cargo <command>` anywhere in your project directory. Example:

```
$ cp target/release/cargo-* ~/.bin
```

In the above example, the `.bin` directory inside my home directy is inside my `$PATH`

###### Linux / OS X

You have two options, place `cargo-count` into a directory that is already located in your `$PATH` variable (To see which directories those are, open a terminal and type `echo "${PATH//:/\n}"`, the quotation marks are important), or you can add a custom directory to your `$PATH`

**Option 1**
If you have write permission to a directory listed in your `$PATH` or you have root permission (or via `sudo`), simply copy the binaries `$ cp target/release/cargo-*` to that directory `# sudo cp target/release/cargo-* /usr/local/bin`

**Option 2**
If you do not have root, `sudo`, or write permission to any directory already in `$PATH` you can create a directory inside your home directory, and add that. Many people use `$HOME/.bin` to keep it hidden (and not clutter your home directory), or `$HOME/bin` if you want it to be always visible. Here is an example to make the directory, add it to `$PATH`, and copy the binaries there.

Simply change `bin` to whatever you'd like to name the directory, and `.bashrc` to whatever your shell startup file is (usually `.bashrc`, `.bash_profile`, or `.zshrc`)

```
$ mkdir ~/bin
$ echo "export PATH=$PATH:$HOME/bin" >> ~/.bashrc
$ cp target/release/cargo-* ~/bin
$ source ~/.bashrc
```

##### Windows

On Windows 7/8 you can add directory to the `PATH` variable by opening a command line as an administrator and running

```
C:\> setx path "%path%;C:\path\to\cargo\binaries"
```

Otherwise, ensure you have the binaries in the directory which you operating in the command line from, because Windows automatically adds your current directory to `PATH` (i.e. if you open a command line to `C:\my_project\\` to use `cargo-count` ensure `cargo-count.exe` is inside that directory as well).

## Included Subcommands

`cargo-extras` currently includes the following subcommands (commits listed for subcommands not using `git tag`s):

 * [cargo-check v0.1.0 (e602882a3a)](https://github.com/rsolomo/cargo-check) - a wrapper around `cargo rustc -- -Zno-trans` which can be helpful for running a faster compile if you only need correctness checks
 * [cargo-config v0.1.1 (d6ad04c593)](https://github.com/wesleywiser/cargo-config) - prints info about the current crate
 * [cargo-count v0.1.3](https://github.com/kbknapp/cargo-count) - lists source code counts and details about cargo projects, including unsafe statistics
 * [cargo-do v0.3.1 (b120fce315)](https://github.com/pwoolcoc/cargo-do) - run multiple `cargo` commands in a row
 * [cargo-edit v0.1.1 (3ae8e70bf1)](https://github.com/killercup/cargo-edit) - allows you to add and remove dependencies from the command line. Installs `cargo-add`, `cargo-rm`, and `cargo-list`.
 * [cargo-fmt v0.1.0 (e24dc7bdfb)](https://github.com/pwoolcoc/cargo-fmt) - allows running [rustfmt](https://github.com/rust-lang-nursery/rustfmt) from `cargo`
 * [cargo-graph v0.2.0](https://github.com/kbknapp/cargo-graph) - builds dependency graphs using GraphViz `dot` and is an updated fork of [cargo-dot](https://github.com/maxsnew/cargo-dot) with additional features
 * [cargo-open v0.3.0 (c070fb01b5)](https://github.com/carols10cents/cargo-open) - quickly open a crate in your `$EDITOR`
 * [cargo-outdated v0.1.3](https://github.com/kbknapp/cargo-outdated) - displays when newer versions of Rust dependencies are available, or out of date
 * [cargo-script v0.1.4 (ccf3f7fbfc)](https://github.com/DanielKeep/cargo-script) - lets people quickly and easily run Rust "scripts" which can make use of Cargo's package ecosystem
 * [cargo-watch v3.0.1](https://github.com/passcod/cargo-watch) - utility for `cargo` to compile projects when sources change

## License

`cargo-extras` is released under the terms of the MIT. See the LICENSE-MIT file for the details. The subcommands themselves may be released under different licenes, see the [src](src) and the binary in question, most commands have a license file included with them.
