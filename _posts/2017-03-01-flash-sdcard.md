---
layout: post
title:  "Configuring Users"
date:   2017-03-01 23:22:08 +0000
categories: jekyll update
---

# Description
This guide aims to describe how to modify the default Raspbian users to something more secure.

# Steps
Let us start by defining the "root" user password.
```
ROOT_PASS='<Root_Password>'
```

Followed by which users we are going to create to become the new "pi".
```
ADMIN_USER='<Administrator_Username>'
ADMIN_PASS='<Administrator_Password>'
```

Modifying the 'root' user default password.
```
sudo passwd 
> $ROOT_PASS
> $ROOT_PASS
```

Add new user and create home folder.
```
sudo useradd -m $ADMIN_USER
```

Set new user password.
```
sudo passwd $ADMIN_USER
> $ADMIN_PASS
> $ADMIN_PASS
```

Make new user a sudoer (admin).
```
echo "$ADMIN_USER    ALL=(ALL:ALL) ALL" | sudo tee /etc/sudoers.d/$ADMIN_USER
sudo chmod 440 /etc/sudoers.d/$ADMIN_USER
```

Remove user 'pi' along with home folder "/home/pi"
```
sudo userdel -r pi
```

Remove user 'pi' sudoer privileges.
```
sudo rm /etc/sudoers.d/010_pi-nopasswd
```

Unset variables
```
unset ADMIN_USER
unset ADMIN_PASS
unset ROOT_PASS
```

# Troubleshooting
Get members of group
```
sudo apt-get update
sudo apt-get install members
members <group>
members www-data
```

Remove user from group
```
deluser <username> <groupname>
deluser Administrator www-data
```

# Add user to group
```
usermod -a -G <group> <user>
usermod -a -G www-data Administrator
```

# References
* [http://unix.stackexchange.com/questions/287620/why-failing-to-delete-user-in-raspbian][stackexchange]
* [http://askubuntu.com/questions/80115/how-to-remove-a-user-from-a-group][askubuntu]
* [https://www.cyberciti.biz/faq/linux-list-all-members-of-a-group/][cyberciti]

[stackexchange]: http://unix.stackexchange.com/questions/287620/why-failing-to-delete-user-in-raspbian
[askubuntu]: http://askubuntu.com/questions/80115/how-to-remove-a-user-from-a-group
[cyberciti]: https://www.cyberciti.biz/faq/linux-list-all-members-of-a-group/