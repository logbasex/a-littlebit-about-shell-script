# a-littlebit-about-shell-script

Learning tracking from: https://tldp.org/LDP/abs/html/

# Shell overview
1. Available shells 
`cat /etc/shells`
2. Current shell
`echo $0`
3. Default shell
`echo $SHELL`

Internal Variable
1. `echo $BASH` (path to binary)
2. `echo $BASHPID | echo $$` (current PID)
3. `echo $BASH_VERSION` (The version of Bash installed on the system)
4. `echo $EDITOR` 
5. `$EUID` ("effective" user ID number) >> diff with $UID
See more: https://tldp.org/LDP/abs/html/internalvariables.html


# Package
1. Dialog
- Simple dialog: `dialog --title "INPUT BOX"   --clear --inputbox "Welcome" 16 5`

# mkdir
Create directory
`mkdir dir0{1..3}`

Create a directory and all its parents
`mkdir -p foo/bar/baz`

Create foo/bar and foo/baz directories
`mkdir -p foo/{bar,baz}`

# rmdir (Remove only empty dir)
# rm (Remove file and dir)

# find

Syntax: find `[where to start searching from]` `[expression determines what to find]` `[what to find]` `[what to do]`

Ex: We find files `[from current directory]` which is `[directory]` with name `['*-cache']` and then `[remove all the found files]`.
```
find . -type d -name '*_cache' -exec rm -r {} +
```
`.`               recursive search in current directory

`-type d`         restricted to search only directory

`-name '*_cache'` search only directories that end with _cache

`-exec`           executes an external command with optional arguments, in this case, that is `rm -r`.

`{} +`            appends the found files to the end of the `rm` command.

Difference between `{} +` and `{} \;` is the first one the `find` command appends found files to the end of the command rather than invoking it once per file (so that the command is run only once, if possible). You can check performance by running these following command:

`time find . -iname '*.jpg' -exec ls {} +`

`time find . -iname '*.jpg' -exec ls {} \;`

# systemd

https://medium.com/@benmorel/creating-a-linux-service-with-systemd-611b5c8b91d6
https://www.linode.com/docs/guides/start-service-at-boot/

