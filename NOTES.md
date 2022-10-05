#  bash

## Build
Bash variables:

## [Loadable Builtin Extensions](_build/lib/bash)

To load from `$LOADABLE_BUILTINS_PATH`:

````shell
export LOADABLE_BUILTINS_PATH="${PREFIX}/lib/bash"
enable -f realpath realpath
`````
or, `enable -f "${PREFIX}/lib/bash/realpath" realpath`

### List of all loadables
````shell
find "${PREFIX}/lib/bash/examples/loadables" -type f -name "*.c" | \
  xargs awk -F '"' '/^struct builtin / { getline; print $2 }'
````

````shell
enable -f ./mypid enable_mypid
````
* accept
* cat 
## [completions](https://github.com/scop/bash-completion)

### Install
Brew replaces before build and install in `share/bash-completion/bash-completion` *helper library*:
* "readlink -f" with "readlink"
* ":-/etc/bash_completion.d" with ":-/usr/local/etc/bash_completion.d"

and, 
````shell
autoreconf -i  # if not installing from prepared release tarball
./configure
make           # GNU make required
make check     # optional, requires python3 with pytest >= 3.6, pexpect
make install   # as root,
````

installation uses:
* `${sysconfdir}/profile.d/bash_completion.sh` for the 
[sourcing helper](https://github.com/scop/bash-completion/blob/master/bash_completion.sh.in) (brew symlink)
* `${datadir}/bash_completion.d` as compat dir, and
* sed `${datadir}/bash-completion/bash_completion` with the prefixes.

[sourcing helper](https://github.com/scop/bash-completion/blob/master/bash_completion.sh.in) 
is installed if `make install` or symlinked in case of brew.

### [Configure/Environment Variables](https://github.com/scop/bash-completion/blob/master/doc/configuration.md)

## Bash Variables and helper function
Bash sets the following variables:
   * macOS:
     1. HOSTTYPE=x86_64
     2. MACHTYPE=x86_64-apple-darwin21.6.0
     3. OSTYPE=darwin21.6.0
   * msi, for instance:
   * Linux:
     1. HOSTTYPE=x86_64
     2. MACHTYPE=x86_64-pc-linux-gnu
     3. OSTYPE=linux-gnu

[config.guess](support/config.guess) is generated when `./configure` and outputs `$MACHTYPE` (`${host_cpu}-${host_vendor}-${host_os}`).

`BASHVERS=5.2; RELSTATUS=release` are hard coded in [configure](configure) script.

[config.sub](support/config.sub) has the list of all architecture/--host alternatives and checks 
if it is valid and returns the `$MACHTYPE` to use for --host `config.sub x86_64-apple-darwin`, 
aliases can be used: x86_64, amd64, arm64-*, x86_64-linux, x86_64-apple

GitHub actions has `$RUNNER_ARCH` x86, x64 (x86_64), ARM or ARM64 and `$RUNNER_OS` Linux, macOS, Windows.


### CAVEATS

Only files with *.in are used: 
* config.h.in

