ls -> list the contents of a directory.
ls -a -> lists hidden files / folders too.

sudo -> run commands with elevated privileges.
e.g., non-root users cannot install packages. so you need to be an elevated user to install packages. However, you can use the sudo command to get elevated privileges and install packages.

```
(root-user) $> apt install <pkg> -> working
(non-root-user) $> apt install <pkg> -> permission denied
(non-root-user) $> sudo apt install <pkg> -> working
```