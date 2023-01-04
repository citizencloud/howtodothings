## Use `GoPass` 
* [application website](https://www.gopass.pw/)

* if on ubuntu, recommend installing straight from the deb package

```
wget https://github.com/gopasspw/gopass/releases/download/v1.15.0/gopass_1.15.0_linux_amd64.deb && \\
sudo dpkg -i gopass_1.15.0_linux_amd64.deb
```


## Move secret keys from machine to machine

[gpg cheatsheet, facts](http://irtfweb.ifa.hawaii.edu/~lockhart/gpg/)

1. Figure out what GPG keys exist on that machine.

```
gpg --list-secret-keys
```

should return something like ....

```

sec   rsa4096 2019-11-15 [SC]
      2076C7F55907C1981CAF110025F4CA9F99EDAA93
uid           [ultimate] christopherwhitfield (ignorance) <whitfield.christopher.m@gmail.com>
ssb   rsa4096 2019-11-15 [E]

```


2. Export the relevant key using the `email` as the name. To export the above key, would type:

```
gpg --export-secret-key "whitfield.christopher.m@gmail.com" > key_backup.asc
```

if the key was password encrypted, the above command should prompt you to enter that password. type it in successfully and there will exist
a file containing 4096 bits of hex digits which is the actual thing that you must keep secret, must keep safe.


3. That key then should be moved onto whatever devices you want to access your password store from. Manually move it to that device (flash drive and then delete from flash drive) and run the command:

```
gpg --import key_backup.asc
```

## Initialize an existing store from github

* Take an `initialized` password-store that exists as a git repo, i.e. [secretbox](https://github.com/citizencloud/passwordstore)
* Clone it!


**The below command will clone the password store as is to the root password store**

```
gopass clone git@github.com:citizencloud/passwordstore.git
```

**However when using multiple stores, you may wish to use a custom, non-default root mount for your store. To do so:**

```
gopass clone git@github.com:citizencloud/passwordstore.git monk
```

The above command initializes the password store in the `~/.local/share/gopass/stores/monk` directory.

**REMEMBER** to be able to use this non-root password store, you have to mount it!

```
gopass mounts add monk
```
