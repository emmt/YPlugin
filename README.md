# YPlugin

This is a simple script to help you creating a Git repository for a
[Yorick](http://yorick.github.com/) plug-in.

Compared to the standard:
```
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
```
./create [-h|--help] [OPTIONS] [--] NAME DESTDIR
```
to create an initial Git repository for Yorick plugin `NAME` in directory
`DESTDIR` which must not already exists.

Possible options are:
* `--author=AUTHOR`      Author(s) of this software.
* `--email=EMAIL`        Email address to join the author(s).
* `--descr=DESCR`        Short description of this software
* `--license=mit|gpl|lgpl|cecill|cecill-b|cecill-c|none`
                         Type of license.
* `--cflags=CFLAGS`      Default compiler flags.
* `--deplibs=DEPLIBS`    Default flags for dependencies.
* `--ldflags=LDFLAGS`    Default linker flags [].
* `--debug`              Debug mode.
* `-h`, `--help`         Print help and exit.

The default license is `MIT`, you can specify `none` to not choose an
initial license.  If unspecified, the author name and email are guessed
from the global Git configuration parameters or from the informations
available in `/etc/passwd`.  If not yet done, you may set these with:
```
git config --global --add user.name NAME
git config --global --add user.email EMAIL
```

If you accept the settings, the `create` script make the `DESTDIR` and
populate it with some initial files.  Instructions in the `README.md` file
explain how to use the `configure` script to build the plug-in.


