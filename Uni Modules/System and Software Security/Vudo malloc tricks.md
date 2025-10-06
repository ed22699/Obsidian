---
tags:
  - Article
---
## Introduction
- even a single byte located somewhere in the heap, erroneously overwritten by a NUL byte before a call to syslog(3) and immediately restored after the syslog(3) call, may actually lead to execution of arbitrary code as root
- article focuses on Linux/Intel systems
## Potential security problem
### A real problem
#### The vulnerable function
- `do_syslog()` can be found in the logging.c file
	- called by `log_auth()` and `log_error()`, in order to syslog allow/deny and error messages
	- if message is longer than `MAXSYSLOGLEN` (960) characters,`do_syslog()` splits it into parts, breaking up the line into what will fit on one syslog line (at most `MAXSYSLOGLEN` characters) and trying to break on a word boundary if possible
```c
/*
 * Log a message to syslog, pre-pending the username and splitting the
 * message into parts if it is longer than MAXSYSLOGLEN.
 */
static void do_syslog( int pri, char * msg )
{
    int count;
    char * p;
    char * tmp;
    char save;

    /*
     * Log the full line, breaking into multiple syslog(3) calls if
     * necessary
     */
[1] for ( p=msg, count=0; count < strlen(msg)/MAXSYSLOGLEN + 1; count++ ) {
[2]     if ( strlen(p) > MAXSYSLOGLEN ) {
            /*
             * Break up the line into what will fit on one syslog(3) line
             * Try to break on a word boundary if possible.
             */
[3]         for ( tmp = p + MAXSYSLOGLEN; tmp > p && *tmp != ' '; tmp-- )
                ;
            if ( tmp <= p )
[4]             tmp = p + MAXSYSLOGLEN;

            /* NULL terminate line, but save the char to restore later */
            save = *tmp;
[5]         *tmp = '\0';

            if ( count == 0 )
                SYSLOG( pri, "%8.8s : %s", user_name, p );
            else
                SYSLOG( pri,"%8.8s : (command continued) %s",user_name,p );

            /* restore saved character */
[6]         *tmp = save;

            /* Eliminate leading whitespace */
[7]         for ( p = tmp; *p != ' '; p++ )
                ;
[8]     } else {
            if ( count == 0 )
                SYSLOG( pri, "%8.8s : %s", user_name, p );
            else
                SYSLOG( pri,"%8.8s : (command continued) %s",user_name,p );
        }
    }
}
```
#### The segmentation violation
- loop [7] does not check for NUL characters and therefore pushes p way after the end of the NUL terminated character string msg
	- when p reaches the end of the heap Sudo eventually dies with a segmentation violation after an out of-bounds read operation
	- loop [7] has to be run many times n order to reach the end of the heap, the length of the msg string has to be many times `MAXSYSLOGLEN`
### Unreal Exploit
- after the end of the msg buffer is a boundary tag
	- if the Sudo exploit corrupts that boundary tag during execution of `do_syslog()` evil things could happen
### Temporary conclusion
- sudo exploit should
	- overwrite a byte of the boundary tag located after the msg buffer with the NUL byte, therefore control the content of the memory after msg (control of the msg buffer itself is not sufficient)
	- take advantage of the erroneously overwritten byte before it is restored, one of the malloc calls should read the corrupted boundary tag and further alter the usual execution of Sudo
## Doug Lea's Malloc
- malloc is the memory allocator used by the GNU C Library
	- manages the heap and therefore provides the calloc, malloc, free and realloc functions which allocate and free dynamic memory
### A memory allocator
- "This is not the fastest, most space-conserving, most portable, or most
tunable malloc ever written. However it is among the fastest while also
being among the most space-conserving, portable and tunable. Consistent
balance across these factors results in a good general-purpose allocator
for malloc-intensive programs."
#### Goals
- goal of allocator are maximising compatibility, portability, tunability, locality, error detection and minimising space, time and anomalies
#### Algorithms
- "While coalescing via boundary tags and best-fit via binning represent
the main ideas of the algorithm, further considerations lead to a
number of heuristic improvements. They include locality preservation,
wilderness preservation, memory mapping".
##### Boundary tags
- chunks of memory carry around size information fields both before and after the chunk. Allows two important capabilities
	- two bordering unused chunks can be coalesced into one larger chunk. Minimises the number of unusable small chunks
	- all chunks can be traversed starting from any known chunk in either a forward or backward direction
- the boundary tag is great for an attack who tries to exploit heap mismanagement 
	- are control structures located in the very middle of a potentially corruptible memory area (the heap), can eventually execute arbitrary code if they are careful
##### Binning
- available chunks are maintained in bins, grouped by size
- searches for available chunks are processed in smallest-first, best-fit order
##### Locality preservation
- if a chunk of the exact desired size is not available, the most recently split-off space is used if it is big enough; otherwise best-fit is used
- essential to the sudo exploit
	- could protect another free memory area that had to remain untouched
##### Wilderness Preservation
- the space bordering the topmost address allocated from the system
	- ass its at the border it is the only chunk that can be arbitrarily extended to be bigger than it is
- treat the wilderness chunk as it is bigger than all others
	- always being used only if no other chunk exists, further avoiding preventable fragmentation 
- pain for an attacker
### Chunks of memory
- heap is divided into contiguous chunks of memory
- heap layout evolves when malloc functions are called
	- no free chunk physically borders one another (always coalesced into one larger chunk)
#### Synopsis of public routines
- allocated and freed via four main public routines
	- `malloc(size_t n)` 
	- `free(Void_t* p)`
	- `realloc(Void_t* p, size_t n)`
	- `calloc(size_t unit, size_t quantity)`
#### Vital statistics
- when user calls malloc to allocate dynamic memory the effective size of the chunk allocated is never equal to the size requested by the user
	- overhead is a result of the presence of boundary tags before and after the buffer returned to the user
- since size of chunk is always a multiple of 8 bytes, and first chunk in the heap is 8 byte aligned, the chunks of memory returned to the user are always aligned on addresses that are multiples of 8 bytes
- each allocated chunk has a hidden overhead of at least 4 bytes, a field of the boundary tag associated with each chunk, holds size and status information 
#### Available chunks
- kept in bins
- top-most available chunk is always free and never included in any bin
- remainder of the most recently split chunk is always free and never included in any bin
### Boundary tags
#### Structure
- allocated chunks
![[Screenshot 2025-10-05 at 00.07.23.png|500]]
- free chunks stored in circular doubly-linked lists
![[Screenshot 2025-10-05 at 00.09.24.png|500]]
#### Size field
- in order to extract the effective size of a chunk p from its size field, `dlmalloc` needs to mask the two status bits and uses `chunksize()` for this purpose
### Bins
- free chunks of memory are stored in circular doubly-linked lists
- one circular doubly-linked list per bin
	- initially empty as at the start the whole heap is composed of one single chunk (the wilderness chunk)
	- bin is nothing more than a pair of pointers serving as the head of the associated doubly-linked list

1.2.2