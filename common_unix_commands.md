# Common Unix Commands

## Network

Find the IP of all connected devices on the wi-fi network

```
$ arp -a
```
Another one that displays routing table is

```
$ netstat -nr
```

## Server



## Shell

### File permissions

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

## Application

Macdown is argubaly the best Markdown editor on Mac at the moment. To open .md files directly from command line, add an alias in `.bashrc`

```
$ alias macdown "open -a MacDown.app"
```
and do:
```
$ macdown awesome_markdown.md
```


***

[Back to HitichHikder's Guide by Herbert](README.md)