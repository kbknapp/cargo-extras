# cargo-extras

A collection of [cargo](https://github.com/rust-lang/cargo) subcommands for use while working on [Rust](https://www.rust-lang.org/) source code and projects. This repository and package aims to make it easy to install all the additional commands at once.

## Installing

You can install all of the subcommands included in `cargo-extras` with a single `cargo install`.

### Prerequisits

Because one of the subcommands requires `cmake` to build, you must have `cmake` installed on your system. Follow your operating system's guidance for installing this package.

### Primary Method: `cargo install`

Simply run:

```
$ cargo install cargo-extras
```

To see all the commands installed:

```
$ cargo --list
```

This may require a nightly version of `cargo` if you get an error about the `install` command not being found. If you are using `multirust`<sup>[1](https://github.com/Diggsey/multirust-rs),[2](https://github.com/brson/multirust)</sup> you could run:

```
$ multirust run nightly cargo install cargo-extras
```

You may also, instead compile and install the traditional way by following the instructions below.

#### OSX Specifc Issue

On El Capitan there is an issue with `openssl-sys` (see [the related issue](https://github.com/sfackler/rust-openssl/issues/255)) which can be solved by running these two commands (assuming you have [Homebrew](http://brew.sh))

```
$ brew install openssl
$ OPENSSL_INCLUDE_DIR=/usr/local/opt/openssl/include cargo install cargo-extras
```

### Alternate Method: Compiling

Follow these instructions to compile `cargo-extras`, then skip down to Installation.

 1. Ensure you have current version of `cargo` and [Rust](https://www.rust-lang.org) installed
 2. Clone the project `$ git clone --depth 50 https://github.com/kbknapp/cargo-extras && cd cargo-extras`
 3. Build the project `$ cargo build --release` (**NOTE:** There is a large performance differnce when compiling without optimizations, so I recommend alwasy using `--release` to enable to them)
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

`cargo-extras` currently includes the following subcommands

 * [cargo-check](https://github.com/rsolomo/cargo-check) - a wrapper around `cargo rustc -- -Zno-trans` which can be helpful for running a faster compile if you only need correctness checks
 * [cargo-config](https://github.com/wesleywiser/cargo-config) - prints info about the current crate
 * [cargo-count](https://github.com/kbknapp/cargo-count) - lists source code counts and details about cargo projects, including unsafe statistics
 * [cargo-do](https://github.com/pwoolcoc/cargo-do) - run multiple `cargo` commands in a row
 * [cargo-edit](https://github.com/killercup/cargo-edit) - allows you to add and remove dependencies from the command line. Installs `cargo-add`, `cargo-rm`, and `cargo-list`.
 * [cargo-fmt](https://github.com/pwoolcoc/cargo-fmt) - allows running [rustfmt](https://github.com/rust-lang-nursery/rustmft) from `cargo`
 * [cargo-graph](https://github.com/kbknapp/cargo-graph) - builds dependency graphs using GraphViz `dot` and is an updated fork of [cargo-dot](https://github.com/maxsnew/cargo-dot) with additional features
 * [cargo-open](https://github.com/carols10cents/cargo-open) - quickly open a crate in your `$EDITOR`
 * [cargo-outdated](https://github.com/kbknapp/cargo-outdated) - displays when newer versions of Rust dependencies are available, or out of date
 * [cargo-script](https://github.com/DanielKeep/cargo-script) - lets people quickly and easily run Rust "scripts" which can make use of Cargo's package ecosystem
 * [cargo-watch](https://github.com/passcod/cargo-watch) - utility for `cargo` to compile projects when sources change

## License

`cargo-extras` is released under the terms of the MIT. See the LICENSE-MIT file for the details. The subcommands themselves may be released under different licenes, see the [src](src) and the binary in question, most commands have a licenese file included with them.
