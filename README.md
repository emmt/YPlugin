# YPlugin

This is a simple script to help you creating a Git repository for a
[Yorick](http://github.com/LLNL/yorick/) plug-in.

Compared to the standard:

```sh
yorick -batch make.i
```

this script populates a directory with initial files (`Makefile`,
`LICENSE.md`, `README.md`, `AUTHORS`, *etc.*), initializes this directory as
a Git repository (with suitable `.gitignore` and `.gitattributes` files)
and provides you with a `configure` script such that configuration, build
and installation are easier for a user (for instance, the plug-in can be
built in a different directory leaving the source tree unchanged).


## Usage

You simply execute the [`create`](./create) script with a few parameters:

```sh
./create [-h|--help] [OPTIONS] [--] NAME [DESTDIR]
```

to create an initial Git repository for Yorick plugin `NAME` in directory
`DESTDIR` which must not already exists.  If `DESTDIR` is not given, it is
taken to be the argument `NAME` (with `/` replaced by `-`).  Note that the
scrip may be executed from anywhere.

Possible options are:
* `--author=AUTHOR`      Author(s) of the plug-in.
* `--email=EMAIL`        Email address to join the author(s).
* `--descr=DESCR`        Short description of the plug-in.
* `--license=mit|gpl|lgpl|cecill|cecill-b|cecill-c|none`
                         Type of license.
* `--cflags=CFLAGS`      Default compiler flags.
* `--deplibs=DEPLIBS`    Default flags for dependencies.
* `--ldflags=LDFLAGS`    Default linker flags.
* `--pkg_i=PKG_I`        Name of Yorick file with plug-in code.
* `--pkg_c=PKG_C`        Name of C file with C code.
* `--debug`              Debug mode.
* `-h`, `--help`         Print help and exit.

The default license is `MIT`, you can specify `none` to not choose an
initial license.  Letter case is not significant for the license.  The
values of `--cflags`, `--deplibs` and `--ldflags` are used to set default
values in the `configure` script of the plug-in.  If unspecified, the
author name and email are guessed from the global Git configuration
parameters or from the informations available in `/etc/passwd`.  If not yet
done, you may set these with:

```sh
git config --global user.name "FULL NAME"
git config --global user.email "EMAIL"
```

If you accept the settings, the `create` script makes the `DESTDIR` and
populates it with some initial files.  Instructions in the `README.md` file
explain how to use the `configure` script to build the plug-in.


## Macros and file names

* `PKG_NAME` is used as the base name for the package dynamically loaded
  library (DLL) and, prefixed by `yk_`, as the name of the function in the
  DLL to call to initialize the plug-in.  Thus letters, digits and
  underscores are the only allowed characters for `PKG_NAME`.  The value of
  this macro is built from the plug-in name converted to lowercase and
  with all sequences of forbidden characters replaced by a single
  underscore.

* Option `--pkg_i=PKG_I` can be used to specify the name of the Yorick
  source file which has to be `#include`d to load the plug-in.  It
  corresponds to macro `PKG_I` in `Makefile`.  The default value is
  `$PKG_NAME.i`.

* Option `--pkg_c=PKG_C` can be used to specify the name of the main
  C file which has to be compiled to make the plug-in.  Its default value
  is `$PKG_NAME.c`.
