# local-wp-ansible

Local development for Wordpress

---

## Requirements

+ vagrant >= 1.7.3
  * https://qiita.com/uhooi/items/fed061205a13bdaaa514
+ installing vagrant-vbguest
```
vagrant plugin install vagrant-vbguest
```

## Initialize

```
git clone git@github.com:nicedchy/local-wp-ansible.git
cd local-wp-ansible
git clone git clone git@github.com:hoge/your_wordpress.git # 任意のWordPressでもOKです
vagrant up
# Access to https://192.168.33.10/
# Fight!
```

## Commands
### Starting
```
vagrant up
```

### Stopping
```
vagrant halt
```

### Restarting
```
vagrant reload
```

### Provisioning
```
vagrant provision
```

### Login
```
vagrant ssh
```

### Logout
```
exit
```

## Trouble Shootings

### Fail Finding Box

if this error is occurred

```
Checking if box 'centos/7' is up to date...
There was a problem while downloading the metadata for your box
to check for updates. This is not an error, since it is usually due
to temporary network problems. This is just a warning. The problem
encountered was:

The requested URL returned error: 404 Not Found

If you want to check for box updates, verify your network connection
is valid and try again.
```

please uncomment below line in Vagrantfile

```
Vagrant::DEFAULT_SERVER_URL.replace('https://vagrantcloud.com')
```

### Fail Mounting Volumes

if this error is occurred

```
Failed to mount folders in Linux guest. This is usually because
the "vboxsf" file system is not available. Please verify that
the guest additions are properly installed in the guest and
can work properly. The command attempted was:

mount -t vboxsf -o uid=`id -u vagrant`,gid=`getent group vagrant | cut -d: -f3` home_vagrant_wordpress /home/vagrant/wordpress
mount -t vboxsf -o uid=`id -u vagrant`,gid=`id -g vagrant` home_vagrant_wordpress /home/vagrant/wordpress

The error output from the last command was:

mount: unknown filesystem type 'vboxsf'
```

please run this command and Restart

```
vagrant vbguest
```

or install VBoxGuestAdditions

https://qiita.com/yokomotod/items/e69d3cc69a1e16704089

http://download.virtualbox.org/virtualbox/

Occurred for initialize, Please provisioning after reloading.
