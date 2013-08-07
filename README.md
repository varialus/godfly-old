godfly
======

Golang on DragonFly BSD

Roadmap
-------

1. Install FreeBSD and DragonFly BSD. I'm using VirtualBox for snapshots.
2. Build Go on FreeBSD and DragonFly BSD at the same time.
3. Compare differences and fix problems in DragonFly BSD.

Reverse Progress Log
------------

* dfly: Rinse. Repeat. Except use git clone http://github.com/varialus/godfly.git .
* FreeBSD: Rinse. Repeat. Except use git clone http://github.com/varialus/godfly.git .
* dfly: Currently fails quickly.
* FreeBSD: ALL TESTS PASS
* ./all.bash
* cd $HOME/go/src/
* dfly: hg clone https://go.googlecode.com/hg/ $GOROOT
* FreeBSD: hg clone https://go.googlecode.com/hg/ $GOROOT
* export GOBIN=$HOME/bin
* export GOOS=freebsd
* export GOARCH=amd64
* export GOROOT=$HOME/go
* mkdir ~/bin
* mkdir ~/go
* bash
* Just to be safe, log out and log back in.
* FreeBSD: pkg_add -r git
* dfly: pkg_radd mercurial
* FreeBSD: pkg_add -r mercurial
* dfly: pkg_radd bison
* FreeBSD: pkg_add -r bison
* dfly: pkg_radd gmake
* FreeBSD: pkg_add -r gmake
* dfly: pkg_radd bash
* FreeBSD: pkg_add -r bash
* I'm currently using the build instructions at the following address. http://forums.freebsd.org/showpost.php?p=50843&postcount=23
* Log in as root.
* Install the latest version of FreeBSD and DragonFly BSD and then take a snapshot.
