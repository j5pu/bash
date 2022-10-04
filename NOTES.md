#  bash

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
### Interesting to enable
accept basename csv cut dirname dsv fdflags finfo getconf head hello id ln logname mkdir mkfifo mktemp  necho pathchk print printenv push rm rmdir seq setpgid sleep stat strftime sync tee true false tty uname unlink whoami

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
