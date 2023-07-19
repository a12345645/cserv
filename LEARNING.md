# Learning Note

## Learning List

## start and stop the process
### start
```
./cserv start
```
It will fork create a new child process and exit the original process.
Write the child process's `pid` to the config file `cserv.pid`.
### stop
```
./cserv stop
```
It will read the `pid` in config file `cserv.pid`.
Then according to the `pid` send the signal to process for `kill`.
Finally, delete the config file.

## mmap
### Definition at man page
#### Synopsis
```
#include <sys/mman.h>

void *mmap(void addr[.length], size_t length, int prot, int flags,
            int fd, off_t offset);
int munmap(void addr[.length], size_t length);
```
#### Description
mmap() creates a new mapping in the virtual address space of the calling process.
If addr is NULL, then the kernel chooses the (page-aligned) address at which to create the mapping;

- The flags argument

MAP_SHARED
Share this mapping.  Updates to the mapping are visible to other processes mapping the same region, and (in the case of file-backed mappings) are carried through to the underlying file.  (To precisely control when updates are carried through to the underlying file requires the use of msync(2).)

MAP_ANON & MAP_ANONYMOUS
The mapping is not backed by any file; its contents are initialized to zero.  The fd argument is ignored; however, some implementations require fd to be -1 if MAP_ANONYMOUS (or MAP_ANON) is specified, and portable applications should ensure this.  The offset argument should be zero. Support for MAP_ANONYMOUS in conjunction with MAP_SHARED was added in Linux 2.4.

### In code
```
void *addr = mmap(NULL, pg_count * get_page_size(), PROT_READ | PROT_WRITE,
                MAP_ANONYMOUS | MAP_SHARED, -1, 0);
```
Create the share mamory space with page-aligned. Declare the memory size align with page size that can decrease the page fault probability.