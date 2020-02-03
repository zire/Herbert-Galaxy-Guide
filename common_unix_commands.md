# Common Unix Commands

## Network

The equivalent of `ipconfig` on Windows

```
$ ifconfig
```

Find the IP of all connected devices on the wi-fi network

```
$ arp -a
```
Another one that displays routing table is

```
$ netstat -nr
```

## Host

Set hostname on Linux. The new host name will become effective on the next login.

```
$ sudo hostnamectl set-hostname new-host-name
```

Set local time zone to open up the menu and select the right one

```
$ sudo dpkg-reconfigure tzdata
```

## Shell

Create a new file

```
$ touch new-file
```

Remove a directory

```
$ rm -rf this-dirctory
```

Find a file or directory

```
$ find . -name 'file-name'
```

Find a tile that contains a string `abc` in its name in the current path recursively

```
$ find . -name "*abc*"
```

Find files that contain string `abcdec` in their content, suggested by a [Stack Overflow post](https://stackoverflow.com/questions/16956810/how-do-i-find-all-files-containing-specific-text-on-linux)

```
$ grep -rnw 'path/to/somewhere' -e 'abcdef'
```
or a simple `grep`

```
$ grep -Ril "abcdef" .
```

Check directory size

```
$ du -sh folder-name
```

Find out the size of each subdirectory in `folder-name`

```
$ du -h folder-name
```

Display current `PATH`

```
$ echo $PATH
```

Add a new path to system variable `PATH`

```
$ export PATH=/path/to/somewhere:$PATH
```

Download a file from URL

```
$ curl -O some_URL_address_for_download_file
```

Clear a messy screen

```
$ clear
```

## Copying & Syncing

When you're on a local computer and try to download a file from a remote server:

```
$ scp username@remote:/file/to/send /where/to/put
```

When you're on a local computer and try to send a file from local computer to a remote server:

```
$ scp /file/to/send username@remote:/where/to/put
```

`scp` can also send files between two remote hosts:

```
$ scp username@remote_1:/file/to/send username@remote_2:/where/to/put
```

Use `rsync` to sync folders and files

```
$ rsync -avzh --stats --progress remoteuser@remoteip  localpath
```

or rsync from local to server

```
$ rsync -avP some_file_name xx.xx.xx.xx:some_directory/
```

rsync from server to local

```
$ rsync -avP xx.xx.xx.xx:some_directory/some_file_name .
```

## File permissions

The three digits of the `chmod` code set permissins for these groups in this order:

- Owner (you)
- Group (a group of other users that you set up)
- World (anyone else browsing around on the file system)

Each digit of this code sets permissions for one of these groups as follows. Read is 4. Write is 2. Execute is 1.

The sums of these numbers give combinations of these permissions:

- 0 = no permissions whatsoever; this person cannot read, write, or execute the file
- 1 = execute only
- 2 = write only
- 3 = write and execute (1+2)
- 4 = read only
- 5 = read and execute (4+1)
- 6 = read and write (4+2)
- 7 = read and write and execute (4+2+1)

Change file permission:

| Command | Purpose |
| --- | --- |
| `chmod 700 apple.txt` | Only you can read, write to, or execute apple.txt |
| `chmod 777 apple.txt` | Everybody can read, write to, or execute apple.txt |
| `chmod 744 apple.txt` | Only you can read, write to, or execute apple.txt; Everybody can read apple.txt |
| `chmod 444 apple.txt` | You can only read apple.txt, as everybody else |

Display the octal permission for a file using the stat command:

```
$ stat -c %a [filename]
```

Display CHMOD Permission in Number Format

```
$ ls -l | awk '{k=0;for(i=0;i<=8;i++)k+=((substr($1,i+2,1)~/[rwx]/) \
*2^(8-i));if(k)printf("%0o ",k);print}'
```

## Application

Macdown is argubaly the best Markdown editor on Mac at the moment. To open .md files directly from command line, add an alias in `.bashrc`

```
$ alias macdown "open -a MacDown.app"
```
and do:
```
$ macdown awesome_markdown.md
```

Install Nix

```
$ curl https://nixos.org/nix/install | sh
```
Then
```
$ . /home/userjoe/.nix-profile/etc/profile.d/nix.sh
```

Search for a package

```
$ nix-env -qa | grep my-package
```

Install the package

```
$ nix-env -i my-package
```

Uninstall the package

```
$ nix-env --uninstall my-package
$ nix-env -e my-package
```

Display installed packages

```
$ nix-env -q
```

Show available packages

```
$ nix-env -qas
```

***

[Back to HitichHikder's Guide by Herbert](README.md)