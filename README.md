godfly
======

Golang on DragonFly BSD

32-bit DragonFly BSD Linux Go Emulation
---------------------------------------

1. Instal 32-bit DragonFly BSD
2. Log in as root
3. kldload linux
4. pkg_radd suse_base
5. ln -s /usr/pkg/emul /compat
6. curl http://go.googlecode.com/files/go1.1.1.linux-386.tar.gz -O
7. mkdir /compat/linux/usr/local
8. tar -C /compat/linux/usr/local -xzf go1.1.1.linux-386.tar.gz
9. brandelf -t Linux /compat/linux/usr/local/go/bin/go
10. /compat/linux/usr/local/go/bin/go version

Roadmap
-------

1. Install FreeBSD and DragonFly BSD. I'm using VirtualBox for snapshots.
2. Build Go on FreeBSD and DragonFly BSD at the same time.
3. Compare differences and fix problems in DragonFly BSD.

Setup
-----

1. Install the latest version of FreeBSD and DragonFly BSD.
2. On FreeBSD use pkg_add -r package_name to install bash, gmake, bison and git.
3. On DragonFly BSD use pkg_radd package_name to install bash, gmake and bison.
4. bash
5. mkdir ~/go
6. mkdir ~/bin
7. export GOROOT=$HOME/go
8. export GOARCH=amd64
9. export GOOS=freebsd or export GOOS=dragonflybsd
10. cd go
11. git clone http://github.com/varialus/godfly.git .
12. cd src
13. ./all.bash
14. Fix errors and push fixes to github.com.
15. cd ..
16. git clean -f
17. rm -r ~/bin
18. mkdir ~/bin
19. git pull
20. Repeat steps 12 through 19.

Notes
-----

* Used FreeBSD specific code as a template.
* Where FreeBSD code doesn't work, used NetBSD code with adjustments to make it work.

Recent Compilation Error
------------------------

\# Building C bootstrap tool.<br />
cmd/dist<br />
\# Building compilers and Go bootstrap tool for host, dragonflybsd/amd64<br />
lib9<br />
libbio<br />
...<br />
pkg/go/build<br />
cmd/go<br />
./make.bash: line 141: 18147 Segmentation fault: 11 (core dumped) "$GOTOOLDIR"/go_bootstrap clean -i std<br />
bash-4.2# Aug  9 00:44:55  kernel: pid 18147 (go_bootstrap), uid 0: exited on signal 11 (core )
