- `make qemu-nox` 실행 오류
```shell
***
*** Error: Couldn't find an i386-*-elf version of GCC/binutils.
*** Is the directory with i386-jos-elf-gcc in your PATH?
*** If your i386-*-elf toolchain is installed with a command
*** prefix other than 'i386-jos-elf-', set your TOOLPREFIX
*** environment variable to that prefix and run 'make' again.
*** To turn off this error, run 'gmake TOOLPREFIX= ...'.
***
gcc -Werror -Wall -o mkfs mkfs.c
make: *** No rule to make target `/usr/include/stdc-predef.h', needed by `cat.o'.  Stop.
```