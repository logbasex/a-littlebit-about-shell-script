# a-littlebit-about-shell-script

Learning tracking from: https://tldp.org/LDP/abs/html/

Internal Variable
1. echo $BASH (path to binary)
2. echo $BASHPID | echo $$ (current PID)
3. echo $BASH_VERSION (The version of Bash installed on the system)
4. echo $EDITOR 
5. $EUID ("effective" user ID number) >> diff with $UID
See more: https://tldp.org/LDP/abs/html/internalvariables.html


# Package
1. Dialog
- Simple dialog: dialog --title "INPUT BOX"   --clear --inputbox "Welcome" 16 5

# mkdir
`Create directory`
mkdir dir0{1..3}
`Create a directory and all its parents`
mkdir -p foo/bar/baz
`Create foo/bar and foo/baz directories`
mkdir -p foo/{bar,baz}

# rmdir (Remove only empty dir)
# rm (Remove file and dir)

# find

```
find . -type d -name '*_cache' -exec rm -r {} +
```
`.`              : recursive search in current directory
`-type d`        : restricted to search only directory
`-name '*_cache'`: search only directories that end with _cache
`-exec`          : executes an external command with optional arguments, in this case, that is `rm -r`.
`{} +`           : appends the found files to the end of the `rm` command.
