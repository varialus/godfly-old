godfly
======

Golang on DragonFly BSD

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
