bash -> Borne again shell

### bash script
bash script is a sequence of commands that can be executed by the bash shell.

### shebang
Shebang (#!) specifies the location of the executable used to run the script. It must me in the first line (not considering comments, newlines and white-spaces).

If you're not sure where the binary might be located, you can use the `which` command to locate the path to the executable, e.g: `which bash` -> `/usr/bin/bash`. You shell will use the binaries in this path to run the script.

If you're using bash shell, then `bash` is the default binary for executing shell script.

If might have seen something line `/usr/bin/env sh` instead of `/usr/bin/bash`. 

You can use `/usr/bin/env` which returns the location of the executable.

Example:
```bash
/usr/bin/env bash # -> /usr/bin/bash
```

