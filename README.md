# a-littlebit-about-shell-script

Learning tracking from: https://tldp.org/LDP/abs/html/

## Shell overview
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


## Package
1. Dialog
- Simple dialog: `dialog --title "INPUT BOX"   --clear --inputbox "Welcome" 16 5`

## Package management
- dpkg (Debian Package)
- apt (Advance Package Tool) #https://itsfoss.com/apt-get-linux-guide/
  - apt-cache (`search` packages)
  - apt-get (`install/upgrade/clean` packages)
    - update (update the database of available packages)
      - Hit: Package is not change
      - Ign: Package is ignore
      - Get: Package has new version
    - upgrade (ONLY install new version of package)
    - disk-upgrade (install new version of package OR remove the older one)
    - remove (don't touch configuration file)
    - purge (remove everything relate to packge, include configuration file)
    - clean
    - autoclean
    - auto remove
    ```
   The `apt` (first release in 2014) command is meant to be pleasant for end users and does not need to be backward compatible like apt-get(8). Therefore some options are different:
   - The option DPkg::Progress-Fancy is enabled.
   - The option APT::Color is enabled.
   - A new list command is available similar to dpkg --list.
   - The option upgrade has --with-new-pkgs enabled by default.
   ```
- aptitude: `sudo apt install -y aptitude`

https://linuxhint.com/debian_package_managers/

## mkdir
Create directory
`mkdir dir0{1..3}`

Create a directory and all its parents
`mkdir -p foo/bar/baz`

Create foo/bar and foo/baz directories
`mkdir -p foo/{bar,baz}`

## rmdir (Remove only empty dir)
## rm (Remove file and dir)

## find

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

## test (The test command is used to check file types and compare values)
test 1 -lt 2 && echo "Yes"


## systemd

https://medium.com/@benmorel/creating-a-linux-service-with-systemd-611b5c8b91d6

https://www.linode.com/docs/guides/start-service-at-boot/

## dmidecode (DMI information reported by BIOS, DMI stand for Desktop Management Interface)
```
Short for Desktop Management Interface, DMI is a framework that enables software to collect information about computer environments across multiple machines in a network.
```

`sudo dmidecode --type 17` (man dmidecode for more)

## lshw (list hardware)

`sudo lshw -short -C memory`

## Thinkpad power tuning

https://austingwalters.com/increasing-battery-life-on-an-arch-linux-laptop-thinkpad-t14s/

https://unix.stackexchange.com/questions/18279/powertop-tunables-what-does-it-do

https://gvisoc.com/tech/linux/2020/04/26/Lenovo-ThinkPad-T490s-a-Battery-Review-under-Linux.html

https://www.reddit.com/r/thinkpad/wiki/os/linux

https://askubuntu.com/questions/112705/how-do-i-make-powertop-changes-permanent

https://gist.github.com/pauloromeira/787c75d83777098453f5c2ed7eafa42a

https://support.system76.com/articles/battery/

# LINUX ARCHIVES

[Bill Gates on making ACPI not work with Linux](https://www.osnews.com/story/17689/bill-gates-on-making-acpi-not-work-with-linux/)


# FILE SYSTEM HIERACHY

Command: `man hier`

[What is the purpose of $HOME/.local](https://stackoverflow.com/questions/30274743/what-is-the-purpose-of-home-local)
  - Install `pip3` package, binary file (exutable file) is located in $HOME/.local, we need to `EXPORT PATH=$PATH:~/.local/bin`
  
**/sys/devices**
  - This directory contains the global device hierarchy of all devices on the system. This directory also contains a platform directory and a system directory. The platform directory contains peripheral devices specific to a particular platform such as device controllers. The system directory contains non-peripheral devices such as CPUs and APICs.
  
  `cat /sys/devices/virtual/dmi/id/sys_vendor`

# UTILITIES

**Default editor**

`sudo update-alternatives --config editor`

# MODES

Linux distros include two modes, GUI(Graphic User Interface) and CLI(Commandline User Interface)

[To access them, use this keyboard shortcut](https://askubuntu.com/posts/66198/edit):

<kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>F1</kbd> (or <kbd>F3</kbd> on 17.10 and newer)

*(changing F1 to F1-F6 to access the terminal that you want)*

To get back to your GUI session (the normal desktop):

<kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>F7</kbd> (or <kbd>F2</kbd> on 17.10 and newer)
