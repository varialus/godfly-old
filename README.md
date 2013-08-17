godfly
======

Golang on DragonFly BSD

Recent Error
------------

### Build Error

\# Building C bootstrap tool.<br />
cmd/dist<br />
\# Building compilers and Go bootstrap tool for host, dragonflybsd/amd64<br />
lib9<br />
libbio<br />
...<br />
pkg/go/build<br />
cmd/go<br />
./make.bash: line 141: 19396 Segmentation fault: 11 (core dumped) "$GOTOOLDIR"/go_bootstrap clean -i std<br />
bash-4.2# Aug  11 16:32:21  kernel: pid 19396 (go_bootstrap), uid 0: exited on signal 11 (core dumped)

### gdb

(gdb) run \[clean -i std\]<br />
Starting program: /root/go/pkg/tool/dragonflybsd_amd64/go_bootstrap<br />
<br />
Program received signal SIGSEGV, Segmentation fault.<br />
runtime.settls () at /root/go/src/pkg/runtime/sys_dragonflybsd.s:260<br />
260             MOVL    $0xf1, 0xf1  // crash<br />
(gdb) bt<br />
\#0  runtime.settls () at /root/go/src/pkg/runtime/sys_dragonfly_amd64.s:260<br />
\#1  0x000000000044b006 in _rt0_go ()<br />
    at /root/go/src/pkg/runtime/asm_amd64.s:58<br />
\#2  0x0000000000000000 in ?? ()<br />
(gdb)

### truss

bash-4.2# truss ../pkg/tool/dragonfly_amd64/go_bootstrap clean -i std<br />
open("/proc/curproc/mem",0x1,0400032600400)      = 3 (0x3)<br />
fcntl(0x3,0x2,0x1)                               = 0 (0x0)<br />
ioctl(3,PIOCBIS,0x21)                            = 0 (0x0)<br />
ioctl(3,PIOCSFL,0x1)                             = 0 (0x0)<br />
execve(<missing argument>,<missing argument>,<missing argument>)sysarch(0x81,0x7ffffffff640)<br />
SIGNAL 11<br />
SIGNAL 11<br />
Process stopped because of:  16<br />
process exit, rval = 139<br />
Segmentation fault: 11<br />
bash-4.2# Aug 17 07:37:51  kernel: pid 22655 (go_bootstrap), uid 0: exited on signal 11 (core dumped)<br />
Aug 17 07:37:51  kernel: pid 22654 (truss), uid 0: exited on signal 11

### Notes

* My plea for help. https://groups.google.com/forum/#!topic/golang-dev/bwF5jTJmybM
* Very related discussion. http://comments.gmane.org/gmane.comp.lang.go.devel/30746
* Started assembly language documentation in src/pkg/runtime/sys_dragonflybsd_amd64.s
* Conversation between Snert and dho at http://go-lang.cat-v.org/irc-logs/go-nuts/2009-11-19
* http://www.dragonflybsd.org/docs/user/GlossaryOfTerms/
* http://www.dragonflybsd.org/features/
* http://gitweb.dragonflybsd.org/dragonfly.git/blob/HEAD:/sys/cpu/i386/include/tls.h
* http://gitweb.dragonflybsd.org/dragonfly.git/blob/HEAD:/sys/cpu/x86_64/include/tls.h
* http://gitweb.dragonflybsd.org/dragonfly.git/blob/HEAD:/sys/sys/tls.h
* http://gitweb.dragonflybsd.org/dragonfly.git/blob/HEAD:/sys/platform/pc64/x86_64/tls.c
* http://gitweb.dragonflybsd.org/dragonfly.git/blob/HEAD:/sys/platform/pc32/i386/tls.c
* http://www.dragonflybsd.org/docs/developer/Locking_and_Synchronization/

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

Files Needing Manual Review
---------------------------

* src/libmach/dragonflybsd.c
* src/pkg/os/stat_dragonflybsd.go
* src/pkg/runtime/defs_dragonflybsd.go
* src/pkg/runtime/os_dragonflybsd.h
* src/pkg/runtime/os_dragonflybsd.c
* src/pkg/runtime/mem_dragonflybsd.c
* src/pkg/runtime/rt0_dragonflybsd_386.s
* src/pkg/runtime/rt0_dragonflybsd_amd64.s
* src/pkg/runtime/signal_dragonflybsd_386.h
* src/pkg/runtime/signal_dragonflybsd_amd64.h
* src/pkg/runtime/signals_dragonflybsd.h
* src/pkg/runtime/sys_dragonflybsd_386.s
* src/pkg/runtime/sys_dragonflybsd_amd64.s
* src/pkg/syscall/syscall_dragonflybsd.go
* src/pkg/syscall/syscall_dragonflybsd_386.go
* src/pkg/syscall/syscall_dragonflybsd_amd64.go
* Any Other Copied Manually-Written-Code
