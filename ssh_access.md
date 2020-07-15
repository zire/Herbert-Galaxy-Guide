# Establish SSH Access between Two Machines

Say, I'm on Machine A ("local") and want to access Machine B ("remote") via SSH without using password. 

### Step 1: make sure remote login option is ON for Machine B

If Machine B is a Mac, go to `System Preferences/Sharing/`, check `Remote Login` to turn it on. 

If remote is a Linux machine, this step can be skipped.

### Step 2: create SSH keys on Machine A

On Machine A, `ssh-keygen` to create a pair of public and private SSH keys. By default the private key will be saved to `~.ssh/id_rsa`. Do not enter anything for passphrase prompt - it will create unnecessary problems. 

Two keys have just been created. `id_rsa` is the private key for Machine A that shall always stay on Machine A; `id_rsa.pub` is the public key for Machine B that matches with `id_rsa` and can be uploaded to other machines to enable passwordless access.

### Step 3: copy Machine A's public SSH key to Machine B

On Machine A, if a `.ssh` folder is not yet created on Machine B, 

`cat ~/.ssh/id_rsa.pub | ssh userjoe@12.34.56.78 "mkdir -p ~/.ssh && cat >>  ~/.ssh/authorized_keys"`

I would still need to enter password for Machine B to get through this step.

If `.ssh` folder already exists on Machine B, then on Machine A,

`cat ~/.ssh/id_rsa.pub | ssh userjoe@12.34.56.78 "cat >>  ~/.ssh/authorized_keys"`

Machine A's public SSH key is now saved in `.ssh/authorized_keys` on Machine B. 

### Step 4: configure SSH on Machine A

On Machine A, `vim ~/.ssh/config` and add this entry to the file:

```
host apollo
	HostName	12.34.56.78
	User		userjoe
```

Now, on Machine A, in order to access Machine B, just

`ssh apollo` to rock and roll.

***

[Back to HitichHikder's Guide by Herbert](README.md)

