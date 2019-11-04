# Use Nix as Package Manager

Download Nix, the Purely Functional Package Manager, from its [official site](https://nixos.org/nix/), which is to run this command in the console:

```
$ curl https://nixos.org/nix/install | sh

```

From its [Nix Package Manager Manual](https://nixos.org/nix/manual/), a few frequent commands are the following.

List what packages are available in the channel

```
$ nix-env -qa
```

List what's been installed

```
# nix-env -qas
```

Search for a package

```
$ nix-env -qa some-package
```

Install a package

```
$ nix-env -i some-package
```

Uninstall a package

```
$ nix-env -e some-package
```

Upgrade a package

```
$ nix-env -u some-package
```

If you are unhappy with the result of a nix-env action, roll it back with:

```
$ nix-env --rollback
```
***

[Back to HitichHikder's Guide by Herbert](README.md)