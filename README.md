godfly
======

Golang on DragonFly BSD

Work on cgo
-----------

There is a problem with cgo, auxiliary C/Go integration, which I'm hoping will be fixed and pushed upstream with plenty of time to review before the Go 1.2 freeze which is scheduled for September 1st.

### Status

* Discussion of proper fix. https://groups.google.com/d/msg/golang-dev/O2ALUcNCTAQ/GhnnMguNFWIJ
* My simple proper fix. https://codereview.appspot.com/13247046/

### Notes

* When building with no environment variable, loadlib() in src/cmd/6l/obj.c gets called within main() toward the end of the build process and results in an error on DragonFly BSD, but on FreeBSD, loadlib() doesn't get called at the same place late in the build process. This error which starts out with a call to loadlib() ends within the "if(sym.sym == nil)" block within ldelf() in src/cmd/ld/ldelf.c.
* Overview of the ld/6l linker. http://golang.org/cmd/ld/
* Overview of how cgo works. http://golang.org/misc/cgo/gmp/gmp.go
* Overview of how cgo works. http://golang.org/src/pkg/runtime/cgocall.c

### Setup

1. Log in as Root
2. pkg_radd bash
3. pkg_radd bison
4. pkg_radd clang
5. pkg_radd gcc
6. pkg_radd gmake
7. pkg_radd git
8. pkg_radd mozilla-rootcerts
9. pkg_radd nano
10. rehash
11. mkdir -p /etc/openssl/certs
12. mozilla-rootcerts install
13. nano /etc/rc.conf
14. hostname="dfly.example.local"
15. Ctrl-X, Y, Enter
16. shutdown -r now
17. Log in as User or Root
18. mkdir ~/go
19. git clone http://github.com/varialus/godfly.git ~/go/
20. bash
21. export CC=clang # Optional. Try both with and without this step.
22. export GO_LDFLAGS="-linkmode external";vidcontrol -h 5000;cd ~/go/;git fetch origin cgo;git reset --hard FETCH_HEAD;git clean -df;cd ~/go/src/;./all.bash
23. exit
24. Push fixes to github.com.
25. Repeat steps 20 through 24

64-bit Instructions
-------------------

1. Log in as Root
2. pkg_radd bash
3. pkg_radd bison
4. pkg_radd clang
5. pkg_radd gcc
6. pkg_radd gmake
7. pkg_radd git
8. pkg_radd mozilla-rootcerts
9. pkg_radd nano
10. rehash
11. mkdir -p /etc/openssl/certs
12. mozilla-rootcerts install
13. nano /etc/rc.conf
14. hostname="dfly.example.local"
15. Ctrl-X, Y, Enter
16. shutdown -r now
17. Log in as User or Root
18. mkdir ~/go
19. git clone http://github.com/varialus/godfly.git ~/go/
20. bash
21. export CC=clang # Optional
22. vidcontrol -h 5000;cd ~/go/;git fetch origin upstream;git reset --hard FETCH_HEAD;git clean -df;cd ~/go/src/;./all.bash

Improve Instructions
--------------------

I'll improve the instructions either after cgo is working or after September 1st, whichever comes first.

* Add system installation instructions.
* Add per session environment variables.
* Add go get wingo instructions, including export GIT_SSL_CAINFO="/etc/ssl/certs/ca-certificates.crt"
* Add Hello World!
