## Atjob
Very own modified Linux [`at`](https://en.wikipedia.org/wiki/At_(Unix)) command.

References:
- Official [Source RPM](http://vault.centos.org/6.8/os/Source/SPackages/at-3.1.10-48.el6.src.rpm) version 3.1.10 on Centos 6.8.
- [Build a RPM Package from Source on CentOS / RedHat](http://www.thegeekstuff.com/2015/02/rpm-build-package-example/)

### 1. Setup environment
- Install tools and dependencies:
```
$ sudo yum update -y
$ sudo yum groupinstall -y "Development tools"
$ sudo yum install -y vim git rpm-build
$ sudo yum install -y flex-devel libselinux-devel pam-devel smtpdaemon
```

- Create directories for RPM building:
```
$ mkdir -p ~/rpmbuild/{BUILD,RPMS,SOURCES,SPECS,SRPMS}
$ echo '%_topdir %(echo $HOME)/rpmbuild' > ~/.rpmmacros
```

### 2. Build
- Clone repo:
```
$ git clone https://github.com/genacrys/atjob
$ cd atjob
```

- Create the RPM File:
```
$ tar -czvf at_3.1.10.tar.gz ./at-3.1.10
$ cp {56atd,at_3.1.10.tar.gz,atd.init,atd.sysconf,test.pl} ~/rpmbuild/SOURCES/
$ cp at.spec ~/rpmbuild/SPECS/
$ cd ~/rpmbuild/SPECS/
$ rpmbuild -ba at.spec
```
