godfly
======

Golang on DragonFly BSD

64-bit Instructions
-------------------

1. Log in as Root
2. pkg_radd bash
3. pkg_radd bison
4. pkg_radd clang
5. pkg_radd gmake
6. pkg_radd mercurial
7. pkg_radd mozilla-rootcerts
8. pkg_radd nano
9. rehash
10. mkdir -p /etc/openssl/certs
11. mozilla-rootcerts install
12. nano /etc/rc.conf
13. hostname="dfly.example.local"
14. Ctrl-X, Y, Enter
15. shutdown -r now
16. Log in as User or Root
17. bash
18. vidcontrol -h 5000
19. mkdir ~/go
20. hg clone https://go.googlecode.com/hg/ ~/go/
21. export CC=clang
22. cd ~/go/src/
23. ./all.bash

Tomorrow or the Day After
-------------------------

* Add system installation instructions.
* Add per session environment variables.
* Add go get package, including export GIT_SSL_CAINFO="/etc/ssl/certs/ca-certificates.crt"
* Add wingo instructions.
