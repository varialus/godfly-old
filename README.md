godfly
======

Golang on DragonFly BSD

Status
------

* Go code can be compiled and run!
* The go tool gets built.
* Tests finish running although some are temporarily disabled.
* Thanks to dho, joris and everyone else who helped!
* ???? cmd/cgo
* pass cmd/fix
* pass cmd/go
* pass cmd/gofmt
* ???? cmd/yacc
* fail archive/tar
* ???? archive/zip
* pass bufio
* pass bytes
* ???? compress/bzip
* pass compress/flate
* pass compress/gzip
* pass compress/lzw
* pass container/heap
* pass container/list
* pass container/ring
* ???? crypto
* pass crypto/aes
* fail crypto/cipher
* pass crypto/des
* ???? crypto/da
* fail crypto/ecdsa
* ???? crypto/elliptic
* pass crypto/hmac
* pass crypto/md5
* fail crypto/rand
* pass crypto/rc4
* ???? crypto/rsa
* pass crypto/sha1
* pass crypto/sha256
* pass crypto/sha512
* pass crypto/subtle
* pass crypto/tls
* fail crypto/x509
* ???? crypto/x509/pkix
* pass database/sql
* pass database/sql/driver
* ???? debug/dwarf
* ???? debug/elf
* ???? debug/gosym
* ???? debug/macho
* ???? debug/pe
* pass encoding/asci85
* pass encoding/asn1
* pass encoding/base32
* pass encoding/base64
* pass encoding/binary
* pass encoding/csv
* pass encoding/gob
* pass encoding/hex
* pass encoding/json
* pass encoding/pem
* pass encoding/xml
* pass errors
* pass expvar
* pass flag
* pass fmt
* pass go/ast
* pass go/build
* pass go/doc
* pass go/format
* pass go/parser
* pass go/printer
* pass go/scanner
* pass go/token
* ???? hash
* pass hash/crc32
* pass hash/crc64
* pass hash/fnv
* pass html
* pass html/template
* pass image
* pass image/color
* pass image/draw
* pass image/gif
* pass image/jpeg
* pass image/png
* pass index/suffixarray
* ???? io
* ???? io/ioutil
* pass log
* ???? log/syslog
* pass math
* pass math/big
* pass math/cmplx
* ???? math/rand
* ???? mime
* ???? mime/multipart
* fail net
* fail net/http
* pass net/http/cgi
* pass net/http/cookiejar
* pass net/http/fcgi
* pass net/http/httptest
* pass net/http/httputil
* ???? net/http/pprof
* pass net/mail
* pass net/rpc
* pass net/rpc/jsonrpc
* pass net/smtp
* pass net/textproto
* pass net/url
* fail os
* fail os/exec
* pass os/signal
* pass os/user
* pass path
* pass path/filepath
* pass reflect
* pass regexp
* pass regexpr/syntax
* fail runtime
* ???? runtime/debug
* ???? runtime/pprof
* ???? runtime/race
* pass sort
* pass strconv
* pass strings
* pass sync
* pass sync/atomic
* pass syscall
* pass testing
* ???? testing/iotest
* pass testing/quick
* pass text/scanner
* pass text/tabwriter
* pass text/template
* pass text/template/parse
* fail time
* pass unicode
* pass unicode/utf16
* pass unicode/utf8
* ???? unsafe

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
7. cd go
8. git clone http://github.com/varialus/godfly.git .
9. cd src
10. ./all.bash
11. Fix errors and push fixes to github.com.
12. cd ..
13. git clean -f
14. rm -r ~/bin
15. mkdir ~/bin
16. git pull
17. Repeat steps 9 through 16.

Notes
-----

* http://golang.org/doc/install/source
* Used FreeBSD specific code as a template.

Auto-Generated Files Needing Git Commit
---------------------------------------

* src/pkg/runtime/defs_dragonflybsd_386.h
* src/pkg/runtime/defs_dragonflybsd_amd64.h
* src/pkg/syscall/zerrors_dragonflybsd_386.go
* src/pkg/syscall/zerrors_dragonflybsd_amd64.go
* src/pkg/syscall/zsyscall_dragonflybsd_386.go
* src/pkg/syscall/zsyscall_dragonflybsd_amd64.go
* src/pkg/syscall/zsysnum_dragonflybsd_386.go
* src/pkg/syscall/zsysnum_dragonflybsd_amd64.go
* src/pkg/syscall/ztypes_dragonflybsd_386.go
* src/pkg/syscall/ztypes_dragonflybsd_amd64.go
* All Other Auto-Generated Files

Go Linux Emulation on 32-bit DragonFly BSD
------------------------------------------

1. Instal 32-bit DragonFly BSD
2. Log in as root
3. kldload linux
4. pkg_radd suse_base
5. ln -s /usr/pkg/emul /compat
6. curl http://go.googlecode.com/files/go1.1.1.linux-386.tar.gz -O
7. mkdir /compat/linux/usr/local
8. tar -C /compat/linux/usr/local -xzf go1.1.1.linux-386.tar.gz
9. brandelf -t Linux /compat/linux/usr/local/go/bin/go
10. /compat/linux/usr/local/go/bin/go env

