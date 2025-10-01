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