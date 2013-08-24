godfly
======

Golang on DragonFly BSD

Work on cgo
-----------

There is a problem with cgo, auxiliary C/Go integration, which I'm hoping will be fixed and pushed upstream with plenty of time to review before the Go 1.2 freeze which is scheduled for September 1st.

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
19. git clone http://go.googlecode.com/hg/ ~/go/
20. bash
21. export CC=clang # Optional. Try both with and without this step.
22. vidcontrol -h 5000;cd ~/go/;git reset --hard;git pull;git checkout cgo;cd ~/go/src/;./all.bash
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
19. git clone http://go.googlecode.com/hg/ ~/go/
20. bash
21. export CC=clang # Optional
22. vidcontrol -h 5000;cd ~/go/;git reset --hard;git pull;git checkout upstream;cd ~/go/src/;./all.bash

Improve Instructions
--------------------

I'll improve the instructions either after cgo is working or after September 1st, whichever comes first.

* Add system installation instructions.
* Add per session environment variables.
* Add go get wingo instructions, including export GIT_SSL_CAINFO="/etc/ssl/certs/ca-certificates.crt"
* Add Hello World!
