---
author: Artem Zhivushko
title: linux.essential
create: 2024-03-27 01:09:21
tags:
  - ZeroToHero
  - DevSecOps
  - linux
---

# 𝗙𝗶𝗹𝗲 𝗮𝗻𝗱 𝗗𝗶𝗿𝗲𝗰𝘁𝗼𝗿𝘆 𝗠𝗮𝗻𝗮𝗴𝗲𝗺𝗲𝗻𝘁

## `ls`: Lists the contents of the current directory

> [!info]- **Примечание**
> Размер каталога не равен нулю.
> Грубо говоря, каталоги - это файлы, в которых находится список файлов каталога.
> Размер тоже не случаен - 4 килобайта (4×1024), что равно блоку памяти, выделяемому для работы с данными.

> [!warning] Пример вывода `ls`: `drwxr-xr-x`
> 
> > [!info]- Типы записей в выводе `ls`:
> > `-` - обычный файл
> > `d` - каталог
> > `l` - символьная ссылка
> > `s` - сокет
> > `p` - файл FIFO (First In, First Out)
> 
> > [!info]- Права доступа:
> > - первая тройка - владелец файла
> > - вторая - пользователи из группы владельца
> > - последняя - все остальные
> > 
> > `r` (чтение), `w` (запись), `x` (исполнение)

```bash
⋊> ~ ls --help

Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options too.
  -a, --all                  do not ignore entries starting with .
  -A, --almost-all           do not list implied . and ..
      --author               with -l, print the author of each file
  -b, --escape               print C-style escapes for nongraphic characters
      --block-size=SIZE      with -l, scale sizes by SIZE when printing them;
                             e.g., \'--block-size=M\'; see SIZE format below

  -B, --ignore-backups       do not list implied entries ending with ~
  -c                         with -lt: sort by, and show, ctime (time of last
                             change of file status information);
                             with -l: show ctime and sort by name;
                             otherwise: sort by ctime, newest first

  -C                         list entries by columns
      --color[=WHEN]         color the output WHEN; more info below
  -d, --directory            list directories themselves, not their contents
  -D, --dired                generate output designed for Emacs\' dired mode
  -f                         list all entries in directory order
  -F, --classify[=WHEN]      append indicator (one of */=>@|) to entries WHEN
      --file-type            likewise, except do not append '*'
      --format=WORD          across -x, commas -m, horizontal -x, long -l,
                             single-column -1, verbose -l, vertical -C

      --full-time            like -l --time-style=full-iso
  -g                         like -l, but do not list owner
      --group-directories-first
                             group directories before files;
                             can be augmented with a --sort option, but any
                             use of --sort=none (-U) disables grouping

  -G, --no-group             in a long listing, don\'t print group names
  -h, --human-readable       with -l and -s, print sizes like 1K 234M 2G etc.
      --si                   likewise, but use powers of 1000 not 1024
  -H, --dereference-command-line
                             follow symbolic links listed on the command line
      --dereference-command-line-symlink-to-dir
                             follow each command line symbolic link
                             that points to a directory

      --hide=PATTERN         do not list implied entries matching shell PATTERN
                             (overridden by -a or -A)

      --hyperlink[=WHEN]     hyperlink file names WHEN
      --indicator-style=WORD
                             append indicator with style WORD to entry names:
                             none (default), slash (-p),
                             file-type (--file-type), classify (-F)

  -i, --inode                print the index number of each file
  -I, --ignore=PATTERN       do not list implied entries matching shell PATTERN
  -k, --kibibytes            default to 1024-byte blocks for file system usage;
                             used only with -s and per directory totals

  -l                         use a long listing format
  -L, --dereference          when showing file information for a symbolic
                             link, show information for the file the link
                             references rather than for the link itself

  -m                         fill width with a comma separated list of entries
  -n, --numeric-uid-gid      like -l, but list numeric user and group IDs
  -N, --literal              print entry names without quoting
  -o                         like -l, but do not list group information
  -p, --indicator-style=slash
                             append / indicator to directories
  -q, --hide-control-chars   print ? instead of nongraphic characters
      --show-control-chars   show nongraphic characters as-is (the default,
                             unless program is \'ls\' and output is a terminal)

  -Q, --quote-name           enclose entry names in double quotes
      --quoting-style=WORD   use quoting style WORD for entry names:
                             literal, locale, shell, shell-always,
                             shell-escape, shell-escape-always, c, escape
                             (overrides QUOTING_STYLE environment variable)

  -r, --reverse              reverse order while sorting
  -R, --recursive            list subdirectories recursively
  -s, --size                 print the allocated size of each file, in blocks
  -S                         sort by file size, largest first
      --sort=WORD            sort by WORD instead of name: none (-U), size (-S),
                             time (-t), version (-v), extension (-X), width

      --time=WORD            select which timestamp used to display or sort;
                               access time (-u): atime, access, use;
                               metadata change time (-c): ctime, status;
                               modified time (default): mtime, modification;
                               birth time: birth, creation;
                             with -l, WORD determines which time to show;
                             with --sort=time, sort by WORD (newest first)

      --time-style=TIME_STYLE
                             time/date format with -l; see TIME_STYLE below
  -t                         sort by time, newest first; see --time
  -T, --tabsize=COLS         assume tab stops at each COLS instead of 8
  -u                         with -lt: sort by, and show, access time;
                             with -l: show access time and sort by name;
                             otherwise: sort by access time, newest first

  -U                         do not sort; list entries in directory order
  -v                         natural sort of (version) numbers within text
  -w, --width=COLS           set output width to COLS.  0 means no limit
  -x                         list entries by lines instead of by columns
  -X                         sort alphabetically by entry extension
  -Z, --context              print any security context of each file
      --zero                 end each output line with NUL, not newline
  -1                         list one file per line
      --help        display this help and exit
      --version     output version information and exit

The SIZE argument is an integer and optional unit (example: 10K is 10*1024).
Units are K,M,G,T,P,E,Z,Y,R,Q (powers of 1024) or KB,MB,... (powers of 1000).
Binary prefixes can be used, too: KiB=K, MiB=M, and so on.

The TIME_STYLE argument can be full-iso, long-iso, iso, locale, or +FORMAT.
FORMAT is interpreted like in date(1).  If FORMAT is FORMAT1<newline>FORMAT2,
then FORMAT1 applies to non-recent files and FORMAT2 to recent files.
TIME_STYLE prefixed with \'posix-\' takes effect only outside the POSIX locale.
Also the TIME_STYLE environment variable sets the default style to use.

The WHEN argument defaults to \'always\' and can also be \'auto\' or \'never\'.

Using color to distinguish file types is disabled both by default and
with --color=never.  With --color=auto, ls emits color codes only when
standard output is connected to a terminal.  The LS_COLORS environment
variable can change the settings.  Use the dircolors(1) command to set it.

Exit status:
 0  if OK,
 1  if minor problems (e.g., cannot access subdirectory),
 2  if serious trouble (e.g., cannot access command-line argument).

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/ls>
or available locally via: info \'(coreutils) ls invocation\'
```

## `pwd`: Prints the full path of the current working directory

```bash
pwd - output the current working directory

pwd [-P | --physical]
pwd [-L | --logical]

DESCRIPTION
NOTE: This page documents the fish builtin pwd.  To see the documentation on the pwd command you might have, use command man pwd.

pwd outputs (prints) the current working directory.

The following options are available:

-L or --logical
       Output the logical working directory, without resolving symlinks (default behavior).

-P or --physical
       Output the physical working directory, with symlinks resolved.

-h or --help
       Displays help about using this command.

SEE ALSO
Navigate directories using the directory history or the directory stack
```

## `cd`: Changes the current working directory

## `mkdir`: Creates a new directory

```bash
⋊> ~ mkdir --help
Usage: mkdir [OPTION]... DIRECTORY...
Create the DIRECTORY(ies), if they do not already exist.

Mandatory arguments to long options are mandatory for short options too.
  -m, --mode=MODE   set file mode (as in chmod), not a=rwx - umask
  -p, --parents     no error if existing, make parent directories as needed,
                    with their file modes unaffected by any -m option.
  -v, --verbose     print a message for each created directory
  -Z                   set SELinux security context of each created directory
                         to the default type
      --context[=CTX]  like -Z, or if CTX is specified then set the SELinux
                         or SMACK security context to CTX
      --help        display this help and exit
      --version     output version information and exit

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/mkdir>
or available locally via: info '(coreutils) mkdir invocation'
```

## `rmdir`: Removes an empty directory

```bash
⋊> ~ rmdir --help

Usage: rmdir [OPTION]... DIRECTORY...
Remove the DIRECTORY(ies), if they are empty.

      --ignore-fail-on-non-empty
                    ignore each failure to remove a non-empty directory
  -p, --parents     remove DIRECTORY and its ancestors;
                    e.g., 'rmdir -p a/b' is similar to 'rmdir a/b a'

  -v, --verbose     output a diagnostic for every directory processed
      --help        display this help and exit
      --version     output version information and exit

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/rmdir>
or available locally via: info '(coreutils) rmdir invocation'
```

## `touch`: Creates a new empty file

```bash
⋊> ~ touch --help

Usage: touch [OPTION]... FILE...
Update the access and modification times of each FILE to the current time.

A FILE argument that does not exist is created empty, unless -c or -h
is supplied.

A FILE argument string of - is handled specially and causes touch to
change the times of the file associated with standard output.

Mandatory arguments to long options are mandatory for short options too.
  -a                     change only the access time
  -c, --no-create        do not create any files
  -d, --date=STRING      parse STRING and use it instead of current time
  -f                     (ignored)
  -h, --no-dereference   affect each symbolic link instead of any referenced
                         file (useful only on systems that can change the
                         timestamps of a symlink)
  -m                     change only the modification time
  -r, --reference=FILE   use this file\'s times instead of current time
  -t STAMP               use [[CC]YY]MMDDhhmm[.ss] instead of current time
      --time=WORD        change the specified time:
                           WORD is access, atime, or use: equivalent to -a
                           WORD is modify or mtime: equivalent to -m
      --help        display this help and exit
      --version     output version information and exit

Note that the -d and -t options accept different time-date formats.

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/touch>
or available locally via: info '(coreutils) touch invocation'
```

## `cp`: Copies files or directories

```bash
⋊> ~ cp --help

Usage: cp [OPTION]... [-T] SOURCE DEST
  or:  cp [OPTION]... SOURCE... DIRECTORY
  or:  cp [OPTION]... -t DIRECTORY SOURCE...
Copy SOURCE to DEST, or multiple SOURCE(s) to DIRECTORY.

Mandatory arguments to long options are mandatory for short options too.
  -a, --archive                same as -dR --preserve=all
      --attributes-only        don\'t copy the file data, just the attributes
      --backup[=CONTROL]       make a backup of each existing destination file
  -b                           like --backup but does not accept an argument
      --copy-contents          copy contents of special files when recursive
  -d                           same as --no-dereference --preserve=links
      --debug                  explain how a file is copied.  Implies -v
  -f, --force                  if an existing destination file cannot be
                                 opened, remove it and try again (this option
                                 is ignored when the -n option is also used)
  -i, --interactive            prompt before overwrite (overrides a previous -n
                                  option)
  -H                           follow command-line symbolic links in SOURCE
  -l, --link                   hard link files instead of copying
  -L, --dereference            always follow symbolic links in SOURCE
  -n, --no-clobber             do not overwrite an existing file (overrides a
                                 -u or previous -i option). See also --update
  -P, --no-dereference         never follow symbolic links in SOURCE
  -p                           same as --preserve=mode,ownership,timestamps
      --preserve[=ATTR_LIST]   preserve the specified attributes
      --no-preserve=ATTR_LIST  don\'t preserve the specified attributes
      --parents                use full source file name under DIRECTORY
  -R, -r, --recursive          copy directories recursively
      --reflink[=WHEN]         control clone/CoW copies. See below
      --remove-destination     remove each existing destination file before
                                 attempting to open it (contrast with --force)
      --sparse=WHEN            control creation of sparse files. See below
      --strip-trailing-slashes  remove any trailing slashes from each SOURCE
                                 argument
  -s, --symbolic-link          make symbolic links instead of copying
  -S, --suffix=SUFFIX          override the usual backup suffix
  -t, --target-directory=DIRECTORY  copy all SOURCE arguments into DIRECTORY
  -T, --no-target-directory    treat DEST as a normal file
  --update[=UPDATE]            control which existing files are updated;
                                 UPDATE={all,none,older(default)}.  See below
  -u                           equivalent to --update[=older]
  -v, --verbose                explain what is being done
  -x, --one-file-system        stay on this file system
  -Z                           set SELinux security context of destination
                                 file to default type
      --context[=CTX]          like -Z, or if CTX is specified then set the
                                 SELinux or SMACK security context to CTX
      --help        display this help and exit
      --version     output version information and exit

ATTR_LIST is a comma-separated list of attributes. Attributes are 'mode' for
permissions (including any ACL and xattr permissions), 'ownership' for user
and group, 'timestamps' for file timestamps, 'links' for hard links, 'context'
for security context, 'xattr' for extended attributes, and 'all' for all
attributes.

By default, sparse SOURCE files are detected by a crude heuristic and the
corresponding DEST file is made sparse as well.  That is the behavior
selected by --sparse=auto.  Specify --sparse=always to create a sparse DEST
file whenever the SOURCE file contains a long enough sequence of zero bytes.
Use --sparse=never to inhibit creation of sparse files.

UPDATE controls which existing files in the destination are replaced.
'all' is the default operation when an --update option is not specified,
and results in all existing files in the destination being replaced.
'none' is similar to the --no-clobber option, in that no files in the
destination are replaced, but also skipped files do not induce a failure.
'older' is the default operation when --update is specified, and results
in files being replaced if they\'re older than the corresponding source file.

When --reflink[=always] is specified, perform a lightweight copy, where the
data blocks are copied only when modified.  If this is not possible the copy
fails, or if --reflink=auto is specified, fall back to a standard copy.
Use --reflink=never to ensure a standard copy is performed.

The backup suffix is '~', unless set with --suffix or SIMPLE_BACKUP_SUFFIX.
The version control method may be selected via the --backup option or through
the VERSION_CONTROL environment variable.  Here are the values:

  none, off       never make backups (even if --backup is given)
  numbered, t     make numbered backups
  existing, nil   numbered if numbered backups exist, simple otherwise
  simple, never   always make simple backups

As a special case, cp makes a backup of SOURCE when the force and backup
options are given and SOURCE and DEST are the same name for an existing,
regular file.

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/cp>
or available locally via: info '(coreutils) cp invocation'
```

## `mv`: Moves or renames files or directories

```bash
⋊> ~ mv --help

Usage: mv [OPTION]... [-T] SOURCE DEST
  or:  mv [OPTION]... SOURCE... DIRECTORY
  or:  mv [OPTION]... -t DIRECTORY SOURCE...
Rename SOURCE to DEST, or move SOURCE(s) to DIRECTORY.

Mandatory arguments to long options are mandatory for short options too.
      --backup[=CONTROL]       make a backup of each existing destination file
  -b                           like --backup but does not accept an argument
      --debug                  explain how a file is copied.  Implies -v
  -f, --force                  do not prompt before overwriting
  -i, --interactive            prompt before overwrite
  -n, --no-clobber             do not overwrite an existing file
If you specify more than one of -i, -f, -n, only the final one takes effect.
      --no-copy                do not copy if renaming fails
      --strip-trailing-slashes  remove any trailing slashes from each SOURCE
                                 argument
  -S, --suffix=SUFFIX          override the usual backup suffix
  -t, --target-directory=DIRECTORY  move all SOURCE arguments into DIRECTORY
  -T, --no-target-directory    treat DEST as a normal file
  --update[=UPDATE]            control which existing files are updated;
                                 UPDATE={all,none,older(default)}.  See below
  -u                           equivalent to --update[=older]
  -v, --verbose                explain what is being done
  -Z, --context                set SELinux security context of destination
                                 file to default type
      --help        display this help and exit
      --version     output version information and exit

UPDATE controls which existing files in the destination are replaced.
'all' is the default operation when an --update option is not specified,
and results in all existing files in the destination being replaced.
'none' is similar to the --no-clobber option, in that no files in the
destination are replaced, but also skipped files do not induce a failure.
'older' is the default operation when --update is specified, and results
in files being replaced if they\'re older than the corresponding source file.

The backup suffix is '~', unless set with --suffix or SIMPLE_BACKUP_SUFFIX.
The version control method may be selected via the --backup option or through
the VERSION_CONTROL environment variable.  Here are the values:

  none, off       never make backups (even if --backup is given)
  numbered, t     make numbered backups
  existing, nil   numbered if numbered backups exist, simple otherwise
  simple, never   always make simple backups

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/mv>
or available locally via: info '(coreutils) mv invocation'
```

## `rm`: Removes files or directories

```bash
⋊> ~ rm --help

Usage: rm [OPTION]... [FILE]...
Remove (unlink) the FILE(s).

  -f, --force           ignore nonexistent files and arguments, never prompt
  -i                    prompt before every removal
  -I                    prompt once before removing more than three files, or
                          when removing recursively; less intrusive than -i,
                          while still giving protection against most mistakes
      --interactive[=WHEN]  prompt according to WHEN: never, once (-I), or
                          always (-i); without WHEN, prompt always
      --one-file-system  when removing a hierarchy recursively, skip any
                          directory that is on a file system different from
                          that of the corresponding command line argument
      --no-preserve-root  do not treat '/' specially
      --preserve-root[=all]  do not remove '/' (default);
                              with 'all', reject any command line argument
                              on a separate device from its parent
  -r, -R, --recursive   remove directories and their contents recursively
  -d, --dir             remove empty directories
  -v, --verbose         explain what is being done
      --help        display this help and exit
      --version     output version information and exit

By default, rm does not remove directories.  Use the --recursive (-r or -R)
option to remove each listed directory, too, along with all of its contents.

To remove a file whose name starts with a '-', for example '-foo',
use one of these commands:
  rm -- -foo

  rm ./-foo

Note that if you use rm to remove a file, it might be possible to recover
some of its contents, given sufficient expertise and/or time.  For greater
assurance that the contents are truly unrecoverable, consider using shred(1).

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/rm>
or available locally via: info '(coreutils) rm invocation'
```

## `find`: Search for files in a directory hierarchy

```bash
⋊> ~ find --help

Usage: find [-H] [-L] [-P] [-Olevel] [-D debugopts] [path...] [expression]

Default path is the current directory; default expression is -print.
Expression may consist of: operators, options, tests, and actions.

Operators (decreasing precedence; -and is implicit where no others are given):
      ( EXPR )   ! EXPR   -not EXPR   EXPR1 -a EXPR2   EXPR1 -and EXPR2
      EXPR1 -o EXPR2   EXPR1 -or EXPR2   EXPR1 , EXPR2

Positional options (always true):
      -daystart -follow -nowarn -regextype -warn

Normal options (always true, specified before other expressions):
      -depth -files0-from FILE -maxdepth LEVELS -mindepth LEVELS
      -mount -noleaf -xdev -ignore_readdir_race -noignore_readdir_race
      -xautofs

Tests (N can be +N or -N or N):
      -amin N -anewer FILE -atime N -cmin N -cnewer FILE -context CONTEXT
      -ctime N -empty -false -fstype TYPE -gid N -group NAME -ilname PATTERN
      -iname PATTERN -inum N -iwholename PATTERN -iregex PATTERN
      -links N -lname PATTERN -mmin N -mtime N -name PATTERN -newer FILE
      -nouser -nogroup -path PATTERN -perm [-/]MODE -regex PATTERN
      -readable -writable -executable
      -wholename PATTERN -size N[bcwkMG] -true -type [bcdpflsD] -uid N
      -used N -user NAME -xtype [bcdpfls]

Actions:
      -delete -print0 -printf FORMAT -fprintf FILE FORMAT -print
      -fprint0 FILE -fprint FILE -ls -fls FILE -prune -quit
      -exec COMMAND ; -exec COMMAND {} + -ok COMMAND ;
      -execdir COMMAND ; -execdir COMMAND {} + -okdir COMMAND ;

Other common options:
      --help                   display this help and exit
      --version                output version information and exit

Valid arguments for -D:
exec, opt, rates, search, stat, time, tree, all, help
Use '-D help' for a description of the options, or see find(1)

Please see also the documentation at http://www.gnu.org/software/findutils/.
You can report (and track progress on fixing) bugs in the "find"
program via the GNU findutils bug-reporting page at
https://savannah.gnu.org/bugs/?group=findutils or, if
you have no web access, by sending email to <bug-findutils@gnu.org>.
```

> [!note]- ключ `- type` - тип файла:
> - d - каталог;
> - f - обычный файл;
> - p - именованный файл;
> - l - символьная ссылка (о ссылках - [[ | символьных]] и [[ | жестких]])

> [!attention] Интересная команда для запоминания: 
> `find . -type f -name "*" -print | xargs grep "текст, который ищем"`

# 𝗣𝗿𝗼𝗰𝗲𝘀𝘀 𝗠𝗮𝗻𝗮𝗴𝗲𝗺𝗲𝗻𝘁

## `ps`: Lists currently running processes

```bash
⋊> ~ ps --help all

Usage:
 ps [options]

Basic options:
 -A, -e               all processes
 -a                   all with tty, except session leaders
  a                   all with tty, including other users
 -d                   all except session leaders
 -N, --deselect       negate selection
  r                   only running processes
  T                   all processes on this terminal
  x                   processes without controlling ttys

Selection by list:
 -C <command>         command name
 -G, --Group <GID>    real group id or name
 -g, --group <group>  session or effective group name
 -p, p, --pid <PID>   process id
        --ppid <PID>  parent process id
 -q, q, --quick-pid <PID>
                      process id (quick mode)
 -s, --sid <session>  session id
 -t, t, --tty <tty>   terminal
 -u, U, --user <UID>  effective user id or name
 -U, --User <UID>     real user id or name

  The selection options take as their argument either:
    a comma-separated list e.g. '-u root,nobody' or
    a blank-separated list e.g. '-p 123 4567'

Output formats:
 -F                   extra full
 -f                   full-format, including command lines
  f, --forest         ascii art process tree
 -H                   show process hierarchy
 -j                   jobs format
  j                   BSD job control format
 -l                   long format
  l                   BSD long format
 -M, Z                add security data (for SELinux)
 -O <format>          preloaded with default columns
  O <format>          as -O, with BSD personality
 -o, o, --format <format>
                      user-defined format
  s                   signal format
  u                   user-oriented format
  v                   virtual memory format
  X                   register format
 -y                   do not show flags, show rss vs. addr (used with -l)
     --context        display security context (for SELinux)
     --headers        repeat header lines, one per page
     --no-headers     do not print header at all
     --cols, --columns, --width <num>
                      set screen width
     --rows, --lines <num>
                      set screen height

Show threads:
  H                   as if they were processes
 -L                   possibly with LWP and NLWP columns
 -m, m                after processes
 -T                   possibly with SPID column

Miscellaneous options:
 -c                   show scheduling class with -l option
  c                   show true command name
  e                   show the environment after command
  k,    --sort        specify sort order as: [+|-]key[,[+|-]key[,...]]
  L                   show format specifiers
  n                   display numeric uid and wchan
  S,    --cumulative  include some dead child process data
 -y                   do not show flags, show rss (only with -l)
 -V, V, --version     display version information and exit
 -w, w                unlimited output width

        --help <simple|list|output|threads|misc|all>
                      display help and exit

For more details see ps(1).
```

## `top`: Dynamically displays active processes in real-time

```bash
Help for Interactive Commands - procps-ng 3.3.17
Window 1:Def: Cumulative mode Off.  System: Delay 3.0 secs; Secure mode Off.

  Z,B,E,e   Global: 'Z' colors; 'B' bold; 'E'/'e' summary/task memory scale
  l,t,m,I   Toggle: 'l' load avg; 't' task/cpu; 'm' memory; 'I' Irix mode
  0,1,2,3,4 Toggle: '0' zeros; '1/2/3' cpu/numa views; '4' cpus two abreast
  f,F,X     Fields: 'f'/'F' add/remove/order/sort; 'X' increase fixed-width

  L,&,<,> . Locate: 'L'/'&' find/again; Move sort column: '<'/'>' left/right
  R,H,J,C . Toggle: 'R' Sort; 'H' Threads; 'J' Num justify; 'C' Coordinates
  c,i,S,j . Toggle: 'c' Cmd name/line; 'i' Idle; 'S' Time; 'j' Str justify
  x,y     . Toggle highlights: 'x' sort field; 'y' running tasks
  z,b     . Toggle: 'z' color/mono; 'b' bold/reverse (only if 'x' or 'y')
  u,U,o,O . Filter by: 'u'/'U' effective/any user; 'o'/'O' other criteria
  n,#,^O  . Set: 'n'/'#' max tasks displayed; Show: Ctrl+'O' other filter(s)
  V,v     . Toggle: 'V' forest view; 'v' hide/show forest view children

  k,r       Manipulate tasks: 'k' kill; 'r' renice
  d or s    Set update interval
  W,Y,!     Write config file 'W'; Inspect other output 'Y'; Combine Cpus '!'
  q         Quit
          ( commands shown with '.' require a visible task display window )
Press 'h' or '?' for help with Windows,
Type 'q' or <Esc> to continue
```

## `htop`: An interactive process viewer offering more detailed information

> [!info]- Install:
> `sudo apt-get install htop`
> `yum install htop`
> `sudo dnf install htop`
> `sudo snap install htop`
> `sudo zypper install htop`

```bash
⋊> ~ htop --help

htop 3.3.0
(C) 2004-2019 Hisham Muhammad. (C) 2020-2024 htop dev team.
Released under the GNU GPLv2+.

-C --no-color                   Use a monochrome color scheme
-d --delay=DELAY                Set the delay between updates, in tenths of seconds
-F --filter=FILTER              Show only the commands matching the given filter
-h --help                       Print this help screen
-H --highlight-changes[=DELAY]  Highlight new and old processes
-M --no-mouse                   Disable the mouse
-n --max-iterations=NUMBER      Exit htop after NUMBER iterations/frame updates
-p --pid=PID[,PID,PID...]       Show only the given PIDs
   --readonly                   Disable all system and process changing features
-s --sort-key=COLUMN            Sort by COLUMN in list view (try --sort-key=help for a list)
-t --tree                       Show the tree view (can be combined with -s)
-u --user[=USERNAME]            Show only processes for a given user (or $USER)
-U --no-unicode                 Do not use unicode but plain ASCII
-V --version                    Print version info
   --drop-capabilities[=off|basic|strict] Drop Linux capabilities when running as root
                                off - do not drop any capabilities
                                basic (default) - drop all capabilities not needed by htop
                                strict - drop all capabilities except those needed for
                                         core functionality

Press F1 inside htop for online help.
See 'man htop' for more information.
```

## `kill`: Terminates a specified process

> [!warning] Чтобы прервать любой процесс (неважно, был ли он запущен пользователем root или любым другим пользователем), `kill` и `killall` должны быть выполнены от суперпользователя.

```bash
⋊> ~ kill --help

Usage:
 kill [options] <pid>|<name>...

Forcibly terminate a process.

Options:
 -a, --all              do not restrict the name-to-pid conversion to processes
                          with the same uid as the present process
 -s, --signal <signal>  send this <signal> instead of SIGTERM
 -q, --queue <value>    use sigqueue(2), not kill(2), and pass <value> as data
     --timeout <milliseconds> <follow-up signal>
                        wait up to timeout and send follow-up signal
 -p, --pid              print pids without signaling them
 -l, --list[=<signal>]  list signal names, or convert a signal number to a name
 -L, --table            list signal names and numbers
 -r, --require-handler  do not send signal if signal handler is not present
     --verbose          print pids that will be signaled

 -h, --help             display this help
 -V, --version          display version

For more details see kill(1).
```

> [!warning] `kill` шлет сигнал: не указывая аргументом, какой именно сигнал мы хотим отправить, по умолчанию идет **SIGTERM**. Сигнал сообщает потребность в завершении процесса. Кроме того, процессу предоставляется возможность потенциально остановиться без ошибок, освободив ресурсы. Сложность заключается в том, что сигнал может быть проигнорирован. У всех сигналов есть номер, у SIGTERM, например, 15. Чтобы узнать список всех возможных сигналов и их номеров, нужно ввести следующее: `kill -l`
> 
> > [!bug] Но **SIGTERM** не гарантирует остановку процесса в случае блокировки сигнала или его перехвате. Чтобы наверняка прервать работу процесса без угрозы игнорирования, нужно послать SIGKILL (номер 9) — он немедленно прерывает процесс: `kill −9 279`

> [!info]- Примечание:
> - можно убивать сразу несколько процессов. Для этого указываем их PID подряд через пробел: `kill −9 267 315 442`
> - чтобы не указывать каждый PID по отдельности вручную, можно сделать так: `kill −9 $(pidof gcalctool)`

> [!tip] `pkill` — оболочка для `kill`. Она позволяет применять регулярные выражений или другие критерии для нахождения процессов. У нее такой же синтаксис, как и у команды `kill`, но в качестве PID можно передать имя процесса (или часть его имени). Утилита работает следующим образом: она просматривает директорию proc и находит идентификатор первого процесса с подходящим именем. После этого отправляет этому процессу SIGTERM.

## `killall`: Terminates all instances of a process by name

> [!warning] Чтобы прервать любой процесс (неважно, был ли он запущен пользователем root или любым другим пользователем), `kill` и `killall` должны быть выполнены от суперпользователя.

```bash
⋊> ~ killall -h

Usage: killall [OPTION]... [--] NAME...
       killall -l, --list
       killall -V, --version

  -e,--exact          require exact match for very long names
  -I,--ignore-case    case insensitive process name match
  -g,--process-group  kill process group instead of process
  -y,--younger-than   kill processes younger than TIME
  -o,--older-than     kill processes older than TIME
  -i,--interactive    ask for confirmation before killing
  -l,--list           list all known signal names
  -q,--quiet          don\'t print complaints
  -r,--regexp         interpret NAME as an extended regular expression
  -s,--signal SIGNAL  send this signal instead of SIGTERM
  -u,--user USER      kill only process(es) running as USER
  -v,--verbose        report if the signal was successfully sent
  -V,--version        display version information
  -w,--wait           wait for processes to die
  -n,--ns PID         match processes that belong to the same namespaces
                      as PID
  -Z,--context REGEXP kill only process(es) having context
                      (must precede other arguments)
```

## `pgrep`: Searches for processes by name and prints their PIDs

> [!hint]- **Аналоги**
> `ps axu | grep bash`
> `pidof gcalctool`

```bash
⋊> ~ pgrep --help

Usage:
 pgrep [options] <pattern>

Options:
 -d, --delimiter <string>  specify output delimiter
 -l, --list-name           list PID and process name
 -a, --list-full           list PID and full command line
 -v, --inverse             negates the matching
 -w, --lightweight         list all TID
 -c, --count               count of matching processes
 -f, --full                use full process name to match
 -g, --pgroup <PGID,...>   match listed process group IDs
 -G, --group <GID,...>     match real group IDs
 -i, --ignore-case         match case insensitively
 -n, --newest              select most recently started
 -o, --oldest              select least recently started
 -O, --older <seconds>     select where older than seconds
 -P, --parent <PPID,...>   match only child processes of the given parent
 -s, --session <SID,...>   match session IDs
 -t, --terminal <tty,...>  match by controlling terminal
 -u, --euid <ID,...>       match by effective IDs
 -U, --uid <ID,...>        match by real IDs
 -x, --exact               match exactly with the command name
 -F, --pidfile <file>      read PIDs from file
 -L, --logpidfile          fail if PID file is not locked
 -r, --runstates <state>   match runstates [D,S,Z,...]
 --ns <PID>                match the processes that belong to the same
                           namespace as <pid>
 --nslist <ns,...>         list which namespaces will be considered for
                           the --ns option.
                           Available namespaces: ipc, mnt, net, pid, user, uts

 -h, --help     display this help and exit
 -V, --version  output version information and exit

For more details see pgrep(1).
```

## `pkill`: Terminates processes by name or other criteria

```bash
⋊> ~ pkill --help

Usage:
 pkill [options] <pattern>

Options:
 -<sig>, --signal <sig>    signal to send (either number or name)
 -q, --queue <value>       integer value to be sent with the signal
 -e, --echo                display what is killed
 -c, --count               count of matching processes
 -f, --full                use full process name to match
 -g, --pgroup <PGID,...>   match listed process group IDs
 -G, --group <GID,...>     match real group IDs
 -i, --ignore-case         match case insensitively
 -n, --newest              select most recently started
 -o, --oldest              select least recently started
 -O, --older <seconds>     select where older than seconds
 -P, --parent <PPID,...>   match only child processes of the given parent
 -s, --session <SID,...>   match session IDs
 -t, --terminal <tty,...>  match by controlling terminal
 -u, --euid <ID,...>       match by effective IDs
 -U, --uid <ID,...>        match by real IDs
 -x, --exact               match exactly with the command name
 -F, --pidfile <file>      read PIDs from file
 -L, --logpidfile          fail if PID file is not locked
 -r, --runstates <state>   match runstates [D,S,Z,...]
 --ns <PID>                match the processes that belong to the same
                           namespace as <pid>
 --nslist <ns,...>         list which namespaces will be considered for
                           the --ns option.
                           Available namespaces: ipc, mnt, net, pid, user, uts

 -h, --help     display this help and exit
 -V, --version  output version information and exit

For more details see pgrep(1).
```

## `pstree`: Display a tree of processes

> [!info]- **Install**:
> `apt-get install psmisc`
> `apk add psmisc`
> `pacman -S psmisc`
> `yum install psmisc`
> `dnf install psmisc`
> `sudo zypper in psmisc`
> `brew install pstree`

```bash
⋊> ~ pstree --help

pstree: unrecognized option '--help'
Usage: pstree [-acglpsStTuZ] [ -h | -H PID ] [ -n | -N type ]
              [ -A | -G | -U ] [ PID | USER ]
   or: pstree -V

Display a tree of processes.

  -a, --arguments     show command line arguments
  -A, --ascii         use ASCII line drawing characters
  -c, --compact-not   don\'t compact identical subtrees
  -C, --color=TYPE    color process by attribute
                      (age)
  -g, --show-pgids    show process group ids; implies -c
  -G, --vt100         use VT100 line drawing characters
  -h, --highlight-all highlight current process and its ancestors
  -H PID, --highlight-pid=PID
                      highlight this process and its ancestors
  -l, --long          don\'t truncate long lines
  -n, --numeric-sort  sort output by PID
  -N TYPE, --ns-sort=TYPE
                      sort output by this namespace type
                              (cgroup, ipc, mnt, net, pid, time, user, uts)
  -p, --show-pids     show PIDs; implies -c
  -s, --show-parents  show parents of the selected process
  -S, --ns-changes    show namespace transitions
  -t, --thread-names  show full thread names
  -T, --hide-threads  hide threads, show only processes
  -u, --uid-changes   show uid transitions
  -U, --unicode       use UTF-8 (Unicode) line drawing characters
  -V, --version       display version information
  -Z, --security-context
                      show security attributes

  PID    start at this PID; default is 1 (init)
  USER   show only trees rooted at processes of this user
```

# 𝗨𝘀𝗲𝗿 𝗮𝗻𝗱 𝗚𝗿𝗼𝘂𝗽 𝗠𝗮𝗻𝗮𝗴𝗲𝗺𝗲𝗻𝘁

## `passwd`: Changes a user's password

```bash
⋊> ~ passwd --help

Usage: passwd [options] [LOGIN]

Options:
  -a, --all                     report password status on all accounts
  -d, --delete                  delete the password for the named account
  -e, --expire                  force expire the password for the named account
  -h, --help                    display this help message and exit
  -k, --keep-tokens             change password only if expired
  -i, --inactive INACTIVE       set password inactive after expiration
                                to INACTIVE
  -l, --lock                    lock the password of the named account
  -n, --mindays MIN_DAYS        set minimum number of days before password
                                change to MIN_DAYS
  -q, --quiet                   quiet mode
  -r, --repository REPOSITORY   change password in REPOSITORY repository
  -R, --root CHROOT_DIR         directory to chroot into
  -P, --prefix PREFIX_DIR       directory prefix
  -S, --status                  report password status on the named account
  -u, --unlock                  unlock the password of the named account
  -w, --warndays WARN_DAYS      set expiration warning days to WARN_DAYS
  -x, --maxdays MAX_DAYS        set maximum number of days before password
                                change to MAX_DAYS
```

## `useradd`: Adds a new user to the system

```bash
⋊> ~ useradd

Usage: useradd [options] LOGIN
       useradd -D
       useradd -D [options]

Options:
      --badname                 do not check for bad names
  -b, --base-dir BASE_DIR       base directory for the home directory of the
                                new account
      --btrfs-subvolume-home    use BTRFS subvolume for home directory
  -c, --comment COMMENT         GECOS field of the new account
  -d, --home-dir HOME_DIR       home directory of the new account
  -D, --defaults                print or change default useradd configuration
  -e, --expiredate EXPIRE_DATE  expiration date of the new account
  -f, --inactive INACTIVE       password inactivity period of the new account
  -F, --add-subids-for-system   add entries to sub[ud]id even when adding a system user
  -g, --gid GROUP               name or ID of the primary group of the new
                                account
  -G, --groups GROUPS           list of supplementary groups of the new
                                account
  -h, --help                    display this help message and exit
  -k, --skel SKEL_DIR           use this alternative skeleton directory
  -K, --key KEY=VALUE           override /etc/login.defs defaults
  -m, --create-home             create the user\'s home directory
  -M, --no-create-home          do not create the user\'s home directory
  -N, --no-user-group           do not create a group with the same name as
                                the user
  -o, --non-unique              allow to create users with duplicate
                                (non-unique) UID
  -p, --password PASSWORD       encrypted password of the new account
  -r, --system                  create a system account
  -R, --root CHROOT_DIR         directory to chroot into
  -P, --prefix PREFIX_DIR       prefix directory where are located the /etc/* files
  -s, --shell SHELL             login shell of the new account
  -u, --uid UID                 user ID of the new account
  -U, --user-group              create a group with the same name as the user
  -Z, --selinux-user SEUSER     use a specific SEUSER for the SELinux user mapping
      --selinux-range SERANGE   use a specific MLS range for the SELinux user mapping
```

## `userdel`: Removes a user from the system

```bash
⋊> ~ userdel --help

Usage: userdel [options] LOGIN

Options:
  -f, --force                   force some actions that would fail otherwise
                                e.g. removal of user still logged in
                                or files, even if not owned by the user
  -h, --help                    display this help message and exit
  -r, --remove                  remove home directory and mail spool
  -R, --root CHROOT_DIR         directory to chroot into
  -P, --prefix PREFIX_DIR       prefix directory where are located the /etc/* files
  -Z, --selinux-user            remove any SELinux user mapping for the user
```

## `groups`: Displays the groups a user belongs to

```bash
⋊> ~ groups --help

Usage: groups [OPTION]... [USERNAME]...
Print group memberships for each USERNAME or, if no USERNAME is specified, for
the current process (which may differ if the groups database has changed).
      --help        display this help and exit
      --version     output version information and exit

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/groups>
or available locally via: info '(coreutils) groups invocation'
```

## `usermod`: Modifies user account properties

```bash
⋊> ~ usermod --help

Usage: usermod [options] LOGIN

Options:
  -a, --append                  append the user to the supplemental GROUPS
                                mentioned by the -G option without removing
                                the user from other groups
  -b, --badname                 allow bad names
  -c, --comment COMMENT         new value of the GECOS field
  -d, --home HOME_DIR           new home directory for the user account
  -e, --expiredate EXPIRE_DATE  set account expiration date to EXPIRE_DATE
  -f, --inactive INACTIVE       set password inactive after expiration
                                to INACTIVE
  -g, --gid GROUP               force use GROUP as new primary group
  -G, --groups GROUPS           new list of supplementary GROUPS
  -h, --help                    display this help message and exit
  -l, --login NEW_LOGIN         new value of the login name
  -L, --lock                    lock the user account
  -m, --move-home               move contents of the home directory to the
                                new location (use only with -d)
  -o, --non-unique              allow using duplicate (non-unique) UID
  -p, --password PASSWORD       use encrypted password for the new password
  -P, --prefix PREFIX_DIR       prefix directory where are located the /etc/* files
  -r, --remove                  remove the user from only the supplemental GROUPS
                                mentioned by the -G option without removing
                                the user from other groups
  -R, --root CHROOT_DIR         directory to chroot into
  -s, --shell SHELL             new login shell for the user account
  -u, --uid UID                 new UID for the user account
  -U, --unlock                  unlock the user account
  -v, --add-subuids FIRST-LAST  add range of subordinate uids
  -V, --del-subuids FIRST-LAST  remove range of subordinate uids
  -w, --add-subgids FIRST-LAST  add range of subordinate gids
  -W, --del-subgids FIRST-LAST  remove range of subordinate gids
  -Z, --selinux-user SEUSER     new SELinux user mapping for the user account
      --selinux-range SERANGE   new SELinux MLS range for the user account
```

## `id`: Displays user and group ID information

```bash
⋊> ~ id --help

Usage: id [OPTION]... [USER]...
Print user and group information for each specified USER,
or (when USER omitted) for the current process.

  -a             ignore, for compatibility with other versions
  -Z, --context  print only the security context of the process
  -g, --group    print only the effective group ID
  -G, --groups   print all group IDs
  -n, --name     print a name instead of a number, for -ugG
  -r, --real     print the real ID instead of the effective ID, with -ugG
  -u, --user     print only the effective user ID
  -z, --zero     delimit entries with NUL characters, not whitespace;
                   not permitted in default format
      --help        display this help and exit
      --version     output version information and exit

Without any OPTION, print some useful set of identified information.

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/id>
or available locally via: info '(coreutils) id invocation'
```

## `groupadd`: Creates a new group

```bash
⋊> ~ groupadd

Usage: groupadd [options] GROUP

Options:
  -f, --force                   exit successfully if the group already exists,
                                and cancel -g if the GID is already used
  -g, --gid GID                 use GID for the new group
  -h, --help                    display this help message and exit
  -K, --key KEY=VALUE           override /etc/login.defs defaults
  -o, --non-unique              allow to create groups with duplicate
                                (non-unique) GID
  -p, --password PASSWORD       use this encrypted password for the new group
  -r, --system                  create a system account
  -R, --root CHROOT_DIR         directory to chroot into
  -P, --prefix PREFIX_DIR       directory prefix
  -U, --users USERS             list of user members of this group
```

## `groupdel`: Deletes a group

```bash
⋊> ~ groupdel --help

Usage: groupdel [options] GROUP

Options:
  -h, --help                    display this help message and exit
  -R, --root CHROOT_DIR         directory to chroot into
  -P, --prefix PREFIX_DIR       prefix directory where are located the /etc/* files
  -f, --force                   delete group even if it is the primary group of a user
```

# 𝗦𝘆𝘀𝘁𝗲𝗺 𝗜𝗻𝗳𝗼𝗿𝗺𝗮𝘁𝗶𝗼𝗻

## `uname`: Displays basic system information, such as the operating system name and kernel version

```bash
⋊> ~ uname --help

Usage: uname [OPTION]...
Print certain system information.  With no OPTION, same as -s.

  -a, --all                print all information, in the following order,
                             except omit -p and -i if unknown:
  -s, --kernel-name        print the kernel name
  -n, --nodename           print the network node hostname
  -r, --kernel-release     print the kernel release
  -v, --kernel-version     print the kernel version
  -m, --machine            print the machine hardware name
  -p, --processor          print the processor type (non-portable)
  -i, --hardware-platform  print the hardware platform (non-portable)
  -o, --operating-system   print the operating system
      --help        display this help and exit
      --version     output version information and exit

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/uname>
or available locally via: info '(coreutils) uname invocation'
```

## `df`: Reports disk space usage of file systems

```bash
⋊> ~ df --help

Usage: df [OPTION]... [FILE]...
Show information about the file system on which each FILE resides,
or all file systems by default.

Mandatory arguments to long options are mandatory for short options too.
  -a, --all             include pseudo, duplicate, inaccessible file systems
  -B, --block-size=SIZE  scale sizes by SIZE before printing them; e.g.,
                           '-BM' prints sizes in units of 1,048,576 bytes;
                           see SIZE format below
  -h, --human-readable  print sizes in powers of 1024 (e.g., 1023M)
  -H, --si              print sizes in powers of 1000 (e.g., 1.1G)
  -i, --inodes          list inode information instead of block usage
  -k                    like --block-size=1K
  -l, --local           limit listing to local file systems
      --no-sync         do not invoke sync before getting usage info (default)
      --output[=FIELD_LIST]  use the output format defined by FIELD_LIST,
                               or print all fields if FIELD_LIST is omitted.
  -P, --portability     use the POSIX output format
      --sync            invoke sync before getting usage info
      --total           elide all entries insignificant to available space,
                          and produce a grand total
  -t, --type=TYPE       limit listing to file systems of type TYPE
  -T, --print-type      print file system type
  -x, --exclude-type=TYPE   limit listing to file systems not of type TYPE
  -v                    (ignored)
      --help        display this help and exit
      --version     output version information and exit

Display values are in units of the first available SIZE from --block-size,
and the DF_BLOCK_SIZE, BLOCK_SIZE and BLOCKSIZE environment variables.
Otherwise, units default to 1024 bytes (or 512 if POSIXLY_CORRECT is set).

The SIZE argument is an integer and optional unit (example: 10K is 10*1024).
Units are K,M,G,T,P,E,Z,Y,R,Q (powers of 1024) or KB,MB,... (powers of 1000).
Binary prefixes can be used, too: KiB=K, MiB=M, and so on.

FIELD_LIST is a comma-separated list of columns to be included.  Valid
field names are: 'source', 'fstype', 'itotal', 'iused', 'iavail', 'ipcent',
'size', 'used', 'avail', 'pcent', 'file' and 'target' (see info page).

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/df>
or available locally via: info '(coreutils) df invocation'
```

## `du`: Estimates file and directory space usage

```bash
⋊> ~ du --help

Usage: du [OPTION]... [FILE]...
  or:  du [OPTION]... --files0-from=F
Summarize device usage of the set of FILEs, recursively for directories.

Mandatory arguments to long options are mandatory for short options too.
  -0, --null            end each output line with NUL, not newline
  -a, --all             write counts for all files, not just directories
      --apparent-size   print apparent sizes rather than device usage; although
                          the apparent size is usually smaller, it may be
                          larger due to holes in ('sparse') files, internal
                          fragmentation, indirect blocks, and the like
  -B, --block-size=SIZE  scale sizes by SIZE before printing them; e.g.,
                           '-BM' prints sizes in units of 1,048,576 bytes;
                           see SIZE format below
  -b, --bytes           equivalent to '--apparent-size --block-size=1'
  -c, --total           produce a grand total
  -D, --dereference-args  dereference only symlinks that are listed on the
                          command line
  -d, --max-depth=N     print the total for a directory (or file, with --all)
                          only if it is N or fewer levels below the command
                          line argument;  --max-depth=0 is the same as
                          --summarize
      --files0-from=F   summarize device usage of the
                          NUL-terminated file names specified in file F;
                          if F is -, then read names from standard input
  -H                    equivalent to --dereference-args (-D)
  -h, --human-readable  print sizes in human readable format (e.g., 1K 234M 2G)
      --inodes          list inode usage information instead of block usage
  -k                    like --block-size=1K
  -L, --dereference     dereference all symbolic links
  -l, --count-links     count sizes many times if hard linked
  -m                    like --block-size=1M
  -P, --no-dereference  don\'t follow any symbolic links (this is the default)
  -S, --separate-dirs   for directories do not include size of subdirectories
      --si              like -h, but use powers of 1000 not 1024
  -s, --summarize       display only a total for each argument
  -t, --threshold=SIZE  exclude entries smaller than SIZE if positive,
                          or entries greater than SIZE if negative
      --time            show time of the last modification of any file in the
                          directory, or any of its subdirectories
      --time=WORD       show time as WORD instead of modification time:
                          atime, access, use, ctime or status
      --time-style=STYLE  show times using STYLE, which can be:
                            full-iso, long-iso, iso, or +FORMAT;
                            FORMAT is interpreted like in 'date'
  -X, --exclude-from=FILE  exclude files that match any pattern in FILE
      --exclude=PATTERN    exclude files that match PATTERN
  -x, --one-file-system    skip directories on different file systems
      --help        display this help and exit
      --version     output version information and exit

Display values are in units of the first available SIZE from --block-size,
and the DU_BLOCK_SIZE, BLOCK_SIZE and BLOCKSIZE environment variables.
Otherwise, units default to 1024 bytes (or 512 if POSIXLY_CORRECT is set).

The SIZE argument is an integer and optional unit (example: 10K is 10*1024).
Units are K,M,G,T,P,E,Z,Y,R,Q (powers of 1024) or KB,MB,... (powers of 1000).
Binary prefixes can be used, too: KiB=K, MiB=M, and so on.

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/du>
or available locally via: info '(coreutils) du invocation'
```

## `free`: Displays memory usage information

```bash
⋊> ~ free --help

Usage:
 free [options]

Options:
 -b, --bytes         show output in bytes
     --kilo          show output in kilobytes
     --mega          show output in megabytes
     --giga          show output in gigabytes
     --tera          show output in terabytes
     --peta          show output in petabytes
 -k, --kibi          show output in kibibytes
 -m, --mebi          show output in mebibytes
 -g, --gibi          show output in gibibytes
     --tebi          show output in tebibytes
     --pebi          show output in pebibytes
 -h, --human         show human-readable output
     --si            use powers of 1000 not 1024
 -l, --lohi          show detailed low and high memory statistics
 -t, --total         show total for RAM + swap
 -s N, --seconds N   repeat printing every N seconds
 -c N, --count N     repeat printing N times, then exit
 -C, --full-cache    add further cache lines to main cache
 -w, --wide          wide output

     --help     display this help and exit
 -V, --version  output version information and exit

For more details see free(1).
```

## `lscpu`: Displays CPU architecture information

```bash
⋊> ~ lscpu --help

Usage:
 lscpu [options]

Display information about the CPU architecture.

Options:
 -a, --all               print both online and offline CPUs (default for -e)
 -b, --online            print online CPUs only (default for -p)
 -B, --bytes             print sizes in bytes rather than in human readable format
 -C, --caches[=<list>]   info about caches in extended readable format
 -c, --offline           print offline CPUs only
 -J, --json              use JSON for default or extended format
 -e, --extended[=<list>] print out an extended readable format
 -p, --parse[=<list>]    print out a parsable format
 -s, --sysroot <dir>     use specified directory as system root
 -x, --hex               print hexadecimal masks rather than lists of CPUs
 -y, --physical          print physical instead of logical IDs
     --hierarchic[=when] use subsections in summary (auto, never, always)
     --output-all        print all available columns for -e, -p or -C

 -h, --help              display this help
 -V, --version           display version

Available output columns for -e or -p:
      BOGOMIPS  crude measurement of CPU speed
           CPU  logical CPU number
          CORE  logical core number
        SOCKET  logical socket number
       CLUSTER  logical cluster number
          NODE  logical NUMA node number
          BOOK  logical book number
        DRAWER  logical drawer number
         CACHE  shows how caches are shared between CPUs
  POLARIZATION  CPU dispatching mode on virtual hardware
       ADDRESS  physical address of a CPU
    CONFIGURED  shows if the hypervisor has allocated the CPU
        ONLINE  shows if Linux currently makes use of the CPU
           MHZ  shows the currently MHz of the CPU
      SCALMHZ%  shows scaling percentage of the CPU frequency
        MAXMHZ  shows the maximum MHz of the CPU
        MINMHZ  shows the minimum MHz of the CPU
     MODELNAME  shows CPU model name

Available output columns for -C:
      ALL-SIZE  size of all system caches
         LEVEL  cache level
          NAME  cache name
      ONE-SIZE  size of one cache
          TYPE  cache type
          WAYS  ways of associativity
  ALLOC-POLICY  allocation policy
  WRITE-POLICY  write policy
      PHY-LINE  number of physical cache line per cache tag
          SETS  number of sets in the cache; set lines has the same cache index
 COHERENCY-SIZE  minimum amount of data in bytes transferred from memory to cache

For more details see lscpu(1).
```

## `lshw`: Lists detailed hardware information

> [!info]- **Install**:
> `sudo zypper install lshw`

```bash
⋊> ~ lshw --help

Hardware Lister (lshw) - B.02.19.2+git.20231115
usage: lshw [-format] [-options ...]
       lshw -version

        -version        print program version (B.02.19.2+git.20231115)

format can be
        -html           output hardware tree as HTML
        -xml            output hardware tree as XML
        -json           output hardware tree as a JSON object
        -short          output hardware paths
        -businfo        output bus information

options can be
        -class CLASS    only show a certain class of hardware
        -C CLASS        same as '-class CLASS'
        -c CLASS        same as '-class CLASS'
        -disable TEST   disable a test (like pci, isapnp, cpuid, etc.)
        -enable TEST    enable a test (like pci, isapnp, cpuid, etc.)
        -quiet          don\'t display status
        -sanitize       sanitize output (remove sensitive information like serial numbers, etc.)
        -numeric        output numeric IDs (for PCI, USB, etc.)
        -notime         exclude volatile attributes (timestamps) from output
```

## `lsblk`: Lists information about block devices

> [!info]- **Install**:
> `sudo zypper install util-linux-systemd`

```bash
⋊> ~ lsblk --help

Usage:
 lsblk [options] [<device> ...]

List information about block devices.

Options:
 -A, --noempty        don\'t print empty devices
 -D, --discard        print discard capabilities
 -E, --dedup <column> de-duplicate output by <column>
 -I, --include <list> show only devices with specified major numbers
 -J, --json           use JSON output format
 -M, --merge          group parents of sub-trees (usable for RAIDs, Multi-path)
 -O, --output-all     output all columns
 -P, --pairs          use key="value" output format
 -S, --scsi           output info about SCSI devices
 -N, --nvme           output info about NVMe devices
 -v, --virtio         output info about virtio devices
 -T, --tree[=<column>] use tree format output
 -a, --all            print all devices
 -b, --bytes          print SIZE in bytes rather than in human readable format
 -d, --nodeps         don\'t print slaves or holders
 -e, --exclude <list> exclude devices by major number (default: RAM disks)
 -f, --fs             output info about filesystems
 -i, --ascii          use ascii characters only
 -l, --list           use list format output
 -m, --perms          output info about permissions
 -n, --noheadings     don\'t print headings
 -o, --output <list>  output columns
 -p, --paths          print complete device path
 -r, --raw            use raw output format
 -s, --inverse        inverse dependencies
 -t, --topology       output info about topology
 -w, --width <num>    specifies output width as number of characters
 -x, --sort <column>  sort output by <column>
 -y, --shell          use column names to be usable as shell variable identifiers
 -z, --zoned          print zone related information
     --sysroot <dir>  use specified directory as system root

 -h, --help           display this help
 -V, --version        display version

Available output columns:
    ALIGNMENT  alignment offset
      ID-LINK  the shortest udev /dev/disk/by-id link name
           ID  udev ID (based on ID-LINK)
     DISC-ALN  discard alignment offset
          DAX  dax-capable device
    DISC-GRAN  discard granularity
     DISK-SEQ  disk sequence number
     DISC-MAX  discard max bytes
    DISC-ZERO  discard zeroes data
      FSAVAIL  filesystem size available
      FSROOTS  mounted filesystem roots
       FSSIZE  filesystem size
       FSTYPE  filesystem type
       FSUSED  filesystem size used
       FSUSE%  filesystem use percentage
        FSVER  filesystem version
        GROUP  group name
         HCTL  Host:Channel:Target:Lun for SCSI
      HOTPLUG  removable or hotplug device (usb, pcmcia, ...)
        KNAME  internal kernel device name
        LABEL  filesystem LABEL
      LOG-SEC  logical sector size
      MAJ:MIN  major:minor device number
       MIN-IO  minimum I/O size
         MODE  device node permissions
        MODEL  device identifier
           MQ  device queues
         NAME  device name
       OPT-IO  optimal I/O size
        OWNER  user name
    PARTFLAGS  partition flags
    PARTLABEL  partition LABEL
        PARTN  partition number as read from the partition table
     PARTTYPE  partition type code or UUID
 PARTTYPENAME  partition type name
     PARTUUID  partition UUID
         PATH  path to the device node
      PHY-SEC  physical sector size
       PKNAME  internal parent kernel device name
       PTTYPE  partition table type
       PTUUID  partition table identifier (usually UUID)
           RA  read-ahead of the device
         RAND  adds randomness
          REV  device revision
           RM  removable device
           RO  read-only device
         ROTA  rotational device
      RQ-SIZE  request queue size
        SCHED  I/O scheduler name
       SERIAL  disk serial number
         SIZE  size of the device
        START  partition start offset
        STATE  state of the device
   SUBSYSTEMS  de-duplicated chain of subsystems
   MOUNTPOINT  where the device is mounted
  MOUNTPOINTS  all locations where device is mounted
         TRAN  device transport type
         TYPE  device type
         UUID  filesystem UUID
       VENDOR  device vendor
        WSAME  write same max bytes
          WWN  unique storage identifier
        ZONED  zone model
      ZONE-SZ  zone size
   ZONE-WGRAN  zone write granularity
     ZONE-APP  zone append max bytes
      ZONE-NR  number of zones
    ZONE-OMAX  maximum number of open zones
    ZONE-AMAX  maximum number of active zones

For more details see lsblk(8).
```

# 𝗡𝗲𝘁𝘄𝗼𝗿𝗸 𝗖𝗼𝗻𝗳𝗶𝗴𝘂𝗿𝗮𝘁𝗶𝗼𝗻 𝗮𝗻𝗱 𝗠𝗼𝗻𝗶𝘁𝗼𝗿𝗶𝗻𝗴

## `ifconfig`: Displays and configures network interfaces

> [!bug]- An alternative for `ifconfig` is `ip` и `ss`
```bash
ifconfig --help
Usage:
  ifconfig [-a] [-v] [-s] <interface> [[<AF>] <address>]
  [add <address>[/<prefixlen>]]
  [del <address>[/<prefixlen>]]
  [[-]broadcast [<address>]]  [[-]pointopoint [<address>]]
  [netmask <address>]  [dstaddr <address>]  [tunnel <address>]
  [outfill <NN>] [keepalive <NN>]
  [hw <HW> <address>]  [mtu <NN>]
  [[-]trailers]  [[-]arp]  [[-]allmulti]
  [multicast]  [[-]promisc]
  [mem_start <NN>]  [io_addr <NN>]  [irq <NN>]  [media <type>]
  [txqueuelen <NN>]
  [name <newname>]
  [[-]dynamic]
  [up|down]
```

> [!info]- **Install**:
> `sudo zypper install net-tools-deprecated` или
> `sudo zypper install busybox-net-tools`

## `ip`: Shows and manipulates routing, devices, policy routing, and tunnels

> [!tip] An alternative for `ifconfig` is `ip address `

> [!tip] An alternative for `route -n` is `ip route list`

```bash
⋊> ~ ip --help

Usage: ip [ OPTIONS ] OBJECT { COMMAND | help }
       ip [ -force ] -batch filename
where  OBJECT := { address | addrlabel | amt | fou | help | ila | ioam | l2tp |
                   link | macsec | maddress | monitor | mptcp | mroute | mrule |
                   neighbor | neighbour | netconf | netns | nexthop | ntable |
                   ntbl | route | rule | sr | tap | tcpmetrics |
                   token | tunnel | tuntap | vrf | xfrm }
       OPTIONS := { -V[ersion] | -s[tatistics] | -d[etails] | -r[esolve] |
                    -h[uman-readable] | -iec | -j[son] | -p[retty] |
                    -f[amily] { inet | inet6 | mpls | bridge | link } |
                    -4 | -6 | -M | -B | -0 |
                    -l[oops] { maximum-addr-flush-attempts } | -br[ief] |
                    -o[neline] | -t[imestamp] | -ts[hort] | -b[atch] [filename] |
                    -rc[vbuf] [size] | -n[etns] name | -N[umeric] | -a[ll] |
                    -c[olor]}
```

## `ping`: Tests the reachability of a network host

```bash
⋊> ~ ping -h

Usage
  ping [options] <destination>

Options:
  <destination>      DNS name or IP address
  -a                 use audible ping
  -A                 use adaptive ping
  -B                 sticky source address
  -c <count>         stop after <count> replies
  -C                 call connect() syscall on socket creation
  -D                 print timestamps
  -d                 use SO_DEBUG socket option
  -e <identifier>    define identifier for ping session, default is random for
                     SOCK_RAW and kernel defined for SOCK_DGRAM
                     Imply using SOCK_RAW (for IPv4 only for identifier 0)
  -f                 flood ping
  -h                 print help and exit
  -H                 force reverse DNS name resolution (useful for numeric
                     destinations or for -f), override -n
  -I <interface>     either interface name or address
  -i <interval>      seconds between sending each packet
  -L                 suppress loopback of multicast packets
  -l <preload>       send <preload> number of packages while waiting replies
  -m <mark>          tag the packets going out
  -M <pmtud opt>     define path MTU discovery, can be one of <do|dont|want|probe>
  -n                 no reverse DNS name resolution, override -H
  -O                 report outstanding replies
  -p <pattern>       contents of padding byte
  -q                 quiet output
  -Q <tclass>        use quality of service <tclass> bits
  -s <size>          use <size> as number of data bytes to be sent
  -S <size>          use <size> as SO_SNDBUF socket option value
  -t <ttl>           define time to live
  -U                 print user-to-user latency
  -v                 verbose output
  -V                 print version and exit
  -w <deadline>      reply wait <deadline> in seconds
  -W <timeout>       time to wait for response

IPv4 options:
  -4                 use IPv4
  -b                 allow pinging broadcast
  -R                 record route
  -T <timestamp>     define timestamp, can be one of <tsonly|tsandaddr|tsprespec>

IPv6 options:
  -6                 use IPv6
  -F <flowlabel>     define flow label, default is random
  -N <nodeinfo opt>  use IPv6 node info query, try <help> as argument

For more details see ping(8).
```

## `netstat`: Displays network connections, routing tables, and interface statistics

> [!bug]- An alternative for `netstat` is `ip` и `ss`
> ```bash
> ⋊> ~ netstat --help
> 
> usage: netstat [-vWeenNcCF] [<Af>] -r         netstat {-V|--version|-h|--help}
>        netstat [-vWnNcaeol] [<Socket> ...]
>        netstat { [-vWeenNac] -i | [-cnNe] -M | -s [-6tuw] }
> 
>         -r, --route              display routing table
>         -i, --interfaces         display interface table
>         -g, --groups             display multicast group memberships
>         -s, --statistics         display networking statistics (like SNMP)
>         -M, --masquerade         display masqueraded connections
> 
>         -v, --verbose            be verbose
>         -W, --wide               don\'t truncate IP addresses
>         -n, --numeric            don\'t resolve names
>         --numeric-hosts          don\'t resolve host names
>         --numeric-ports          don\'t resolve port names
>         --numeric-users          don\'t resolve user names
>         -N, --symbolic           resolve hardware names
>         -e, --extend             display other/more information
>         -p, --programs           display PID/Program name for sockets
>         -o, --timers             display timers
>         -c, --continuous         continuous listing
> 
>         -l, --listening          display listening server sockets
>         -a, --all                display all sockets (default: connected)
>         -F, --fib                display Forwarding Information Base (default)
>         -C, --cache              display routing cache instead of FIB
> ```

## `ss`: Another utility for investigating sockets

> [!tip] An alternative for `netstat --numeric --tcp --listen` is `ss --numeric --tcp --listen`

```bash
⋊> ~ ss --help

Usage: ss [ OPTIONS ]
       ss [ OPTIONS ] [ FILTER ]
   -h, --help          this message
   -V, --version       output version information
   -n, --numeric       don\'t resolve service names
   -r, --resolve       resolve host names
   -a, --all           display all sockets
   -l, --listening     display listening sockets
   -o, --options       show timer information
   -e, --extended      show detailed socket information
   -m, --memory        show socket memory usage
   -p, --processes     show process using socket
   -T, --threads       show thread using socket
   -i, --info          show internal TCP information
       --tipcinfo      show internal tipc socket information
   -s, --summary       show socket usage summary
       --tos           show tos and priority information
       --cgroup        show cgroup information
   -b, --bpf           show bpf filter socket information
   -E, --events        continually display sockets as they are destroyed
   -Z, --context       display task SELinux security contexts
   -z, --contexts      display task and socket SELinux security contexts
   -N, --net           switch to the specified network namespace name

   -4, --ipv4          display only IP version 4 sockets
   -6, --ipv6          display only IP version 6 sockets
   -0, --packet        display PACKET sockets
   -t, --tcp           display only TCP sockets
   -M, --mptcp         display only MPTCP sockets
   -S, --sctp          display only SCTP sockets
   -u, --udp           display only UDP sockets
   -d, --dccp          display only DCCP sockets
   -w, --raw           display only RAW sockets
   -x, --unix          display only Unix domain sockets
       --tipc          display only TIPC sockets
       --vsock         display only vsock sockets
       --xdp           display only XDP sockets
   -f, --family=FAMILY display sockets of type FAMILY
       FAMILY := {inet|inet6|link|unix|netlink|vsock|tipc|xdp|help}

   -K, --kill          forcibly close sockets, display what was closed
   -H, --no-header     Suppress header line
   -O, --oneline       socket\'s data printed on a single line
       --inet-sockopt  show various inet socket options

   -A, --query=QUERY, --socket=QUERY
       QUERY := {all|inet|tcp|mptcp|udp|raw|unix|unix_dgram|unix_stream|unix_seqpacket|packet|packet_raw|packet_dgram|netlink|dccp|sctp|vsock_stream|vsock_dgram|tipc|xdp}[,QUERY]

   -D, --diag=FILE     Dump raw information about TCP sockets to FILE
   -F, --filter=FILE   read filter information from FILE
       FILTER := [ state STATE-FILTER ] [ EXPRESSION ]
       STATE-FILTER := {all|connected|synchronized|bucket|big|TCP-STATES}
         TCP-STATES := {established|syn-sent|syn-recv|fin-wait-{1,2}|time-wait|closed|close-wait|last-ack|listening|closing}
          connected := {established|syn-sent|syn-recv|fin-wait-{1,2}|time-wait|close-wait|last-ack|closing}
       synchronized := {established|syn-recv|fin-wait-{1,2}|time-wait|close-wait|last-ack|closing}
             bucket := {syn-recv|time-wait}
                big := {established|syn-sent|fin-wait-{1,2}|closed|close-wait|last-ack|listening|closing}
```

## `traceroute`: Displays the route and transit delays of packets

> [!info]- **Install**:
> `sudo zypper install busybox-traceroute`
> `sudo zypper install traceroute`

```bash
⋊> ~ traceroute --help

BusyBox v1.36.1 () multi-call binary.

Usage: traceroute [-46IFlnrv] [-f 1ST_TTL] [-m MAXTTL] [-q PROBES] [-p PORT]
        [-t TOS] [-w WAIT_SEC] [-s SRC_IP] [-i IFACE]
        [-z PAUSE_MSEC] HOST [BYTES]

Trace the route to HOST

        -4,-6   Force IP or IPv6 name resolution
        -F      Set don\'t fragment bit
        -I      Use ICMP ECHO instead of UDP datagrams
        -l      Display TTL value of the returned packet
        -n      Print numeric addresses
        -r      Bypass routing tables, send directly to HOST
        -v      Verbose
        -f N    First number of hops (default 1)
        -m N    Max number of hops
        -q N    Number of probes per hop (default 3)
        -p N    Base UDP port number used in probes
                (default 33434)
        -s IP   Source address
        -i IFACE Source interface
        -t N    Type-of-service in probe packets (default 0)
        -w SEC  Wait for a response (default 3)
        -z MSEC Wait before each send
```

## `ssh`: Securely logs into remote machines

```bash
⋊> ~ ssh

usage: ssh [-46AaCfGgKkMNnqsTtVvXxYy] [-B bind_interface]
           [-b bind_address] [-c cipher_spec] [-D [bind_address:]port]
           [-E log_file] [-e escape_char] [-F configfile] [-I pkcs11]
           [-i identity_file] [-J [user@]host[:port]] [-L address]
           [-l login_name] [-m mac_spec] [-O ctl_cmd] [-o option] [-p port]
           [-Q query_option] [-R address] [-S ctl_path] [-W host:port]
           [-w local_tun[:remote_tun]] destination [command [argument ...]]
```

## `nc`: A versatile tool for network communication, often dubbed the "Swiss army knife" for TCP/IP

> [!info]- **Install**:
> `sudo zypper install busybox-netcat`
> `sudo zypper install gnu-netcat`
> `sudo zypper install netcat-openbsd`

```bash
⋊> ~ nc

BusyBox v1.36.1 () multi-call binary.

Usage: nc [OPTIONS] HOST PORT  - connect
nc [OPTIONS] -l -p PORT [HOST] [PORT]  - listen

        -e PROG Run PROG after connect (must be last)
        -l      Listen mode, for inbound connects
        -lk     With -e, provides persistent server
        -p PORT Local port
        -s ADDR Local address
        -w SEC  Timeout for connects and final net reads
        -i SEC  Delay interval for lines sent
        -n      Don\'t do DNS resolution
        -u      UDP mode
        -b      Allow broadcasts
        -v      Verbose
        -o FILE Hex dump traffic
        -z      Zero-I/O mode (scanning)
```

## `dig` & `nslookup`: Query Internet name servers interactively

```bash
⋊> ~ dig -h

Usage:  dig [@global-server] [domain] [q-type] [q-class] {q-opt}
            {global-d-opt} host [@local-server] {local-d-opt}
            [ host [@local-server] {local-d-opt} [...]]
Where:  domain    is in the Domain Name System
        q-class  is one of (in,hs,ch,...) [default: in]
        q-type   is one of (a,any,mx,ns,soa,hinfo,axfr,txt,...) [default:a]
                 (Use ixfr=version for type ixfr)
        q-opt    is one of:
                 -4                  (use IPv4 query transport only)
                 -6                  (use IPv6 query transport only)
                 -b address[#port]   (bind to source address/port)
                 -c class            (specify query class)
                 -f filename         (batch mode)
                 -k keyfile          (specify tsig key file)
                 -m                  (enable memory usage debugging)
                 -p port             (specify port number)
                 -q name             (specify query name)
                 -r                  (do not read ~/.digrc)
                 -t type             (specify query type)
                 -u                  (display times in usec instead of msec)
                 -x dot-notation     (shortcut for reverse lookups)
                 -y [hmac:]name:key  (specify named base64 tsig key)
        d-opt    is of the form +keyword[=value], where keyword is:
                 +[no]aaflag         (Set AA flag in query (+[no]aaflag))
                 +[no]aaonly         (Set AA flag in query (+[no]aaflag))
                 +[no]additional     (Control display of additional section)
                 +[no]adflag         (Set AD flag in query (default on))
                 +[no]all            (Set or clear all display flags)
                 +[no]answer         (Control display of answer section)
                 +[no]authority      (Control display of authority section)
                 +[no]badcookie      (Retry BADCOOKIE responses)
                 +[no]besteffort     (Try to parse even illegal messages)
                 +bufsize[=###]      (Set EDNS0 Max UDP packet size)
                 +[no]cdflag         (Set checking disabled flag in query)
                 +[no]class          (Control display of class in records)
                 +[no]cmd            (Control display of command line -
                                      global option)
                 +[no]comments       (Control display of packet header
                                      and section name comments)
                 +[no]cookie         (Add a COOKIE option to the request)
                 +[no]crypto         (Control display of cryptographic
                                      fields in records)
                 +[no]defname        (Use search list (+[no]search))
                 +[no]dns64prefix    (Get the DNS64 prefixes from ipv4only.arpa)
                 +[no]dnssec         (Request DNSSEC records)
                 +domain=###         (Set default domainname)
                 +[no]edns[=###]     (Set EDNS version) [0]
                 +ednsflags=###      (Set EDNS flag bits)
                 +[no]ednsnegotiation (Set EDNS version negotiation)
                 +ednsopt=###[:value] (Send specified EDNS option)
                 +noednsopt          (Clear list of +ednsopt options)
                 +[no]expandaaaa     (Expand AAAA records)
                 +[no]expire         (Request time to expire)
                 +[no]fail           (Don\'t try next server on SERVFAIL)
                 +[no]header-only    (Send query without a question section)
                 +[no]https[=###]    (DNS-over-HTTPS mode) [/]
                 +[no]https-get      (Use GET instead of default POST method while using HTTPS)
                 +[no]http-plain[=###]    (DNS over plain HTTP mode) [/]
                 +[no]http-plain-get      (Use GET instead of default POST method while using plain HTTP)
                 +[no]identify       (ID responders in short answers)
                 +[no]idnin          (Parse IDN names [default=on on tty])
                 +[no]idnout         (Convert IDN response [default=on on tty])
                 +[no]ignore         (Don\'t revert to TCP for TC responses.)
                 +[no]keepalive      (Request EDNS TCP keepalive)
                 +[no]keepopen       (Keep the TCP socket open between queries)
                 +[no]multiline      (Print records in an expanded format)
                 +ndots=###          (Set search NDOTS value)
                 +[no]nsid           (Request Name Server ID)
                 +[no]nssearch       (Search all authoritative nameservers)
                 +[no]onesoa         (AXFR prints only one soa record)
                 +[no]opcode=###     (Set the opcode of the request)
                 +padding=###        (Set padding block size [0])
                 +qid=###            (Specify the query ID to use when sending queries)
                 +[no]qr             (Print question before sending)
                 +[no]question       (Control display of question section)
                 +[no]raflag         (Set RA flag in query (+[no]raflag))
                 +[no]rdflag         (Recursive mode (+[no]recurse))
                 +[no]recurse        (Recursive mode (+[no]rdflag))
                 +retry=###          (Set number of UDP retries) [2]
                 +[no]rrcomments     (Control display of per-record comments)
                 +[no]search         (Set whether to use searchlist)
                 +[no]short          (Display nothing except short
                                      form of answers - global option)
                 +[no]showbadcookie  (Show BADCOOKIE message)
                 +[no]showsearch     (Search with intermediate results)
                 +[no]split=##       (Split hex/base64 fields into chunks)
                 +[no]stats          (Control display of statistics)
                 +subnet=addr        (Set edns-client-subnet option)
                 +[no]tcflag         (Set TC flag in query (+[no]tcflag))
                 +[no]tcp            (TCP mode (+[no]vc))
                 +timeout=###        (Set query timeout) [5]
                 +[no]tls            (DNS-over-TLS mode)
                 +[no]tls-ca[=file]  (Enable remote server\'s TLS certificate validation)
                 +[no]tls-hostname=hostname (Explicitly set the expected TLS hostname)
                 +[no]tls-certfile=file (Load client TLS certificate chain from file)
                 +[no]tls-keyfile=file (Load client TLS private key from file)
                 +[no]trace          (Trace delegation down from root [+dnssec])
                 +tries=###          (Set number of UDP attempts) [3]
                 +[no]ttlid          (Control display of ttls in records)
                 +[no]ttlunits       (Display TTLs in human-readable units)
                 +[no]unknownformat  (Print RDATA in RFC 3597 "unknown" format)
                 +[no]vc             (TCP mode (+[no]tcp))
                 +[no]yaml           (Present the results as YAML)
                 +[no]zflag          (Set Z flag in query)
        global d-opts and servers (before host name) affect all queries.
        local d-opts and servers (after host name) affect only that lookup.
        -h                           (print help and exit)
        -v                           (print version and exit)
```

```bash
# nslookup
```

# 𝗣𝗮𝗰𝗸𝗮𝗴𝗲 𝗠𝗮𝗻𝗮𝗴𝗲𝗺𝗲𝗻𝘁

## `apt-get`, `apt`: Package management tools for Debian-based systems



## `yum`, `dnf`: Package management tools for RPM-based systems



## `rpm`: Package manager for RPM packages (Red Hat Package Manager)



## `dpkg`: Package manager for Debian packages



## `snap`: Universal Linux package system



## `zypper`: Package manager for openSUSE

```bash
⋊> ~ zypper --help

Usage:

    zypper [--GLOBAL-OPTIONS] <COMMAND> [--COMMAND-OPTIONS] [ARGUMENTS]
    zypper <SUBCOMMAND> [--COMMAND-OPTIONS] [ARGUMENTS]

Global Options:

    --help, -h              Help.
    --version, -V           Output the version number.
    --promptids             Output a list of zypper\'s user prompts.
    --config, -c <FILE>     Use specified config file instead of the default.
    --userdata <STRING>     User defined transaction id used in history and plugins.
    --quiet, -q             Suppress normal output, print only error messages.
    --verbose, -v           Increase verbosity.
    --color
    --no-color              Whether to use colors in output if tty supports it.
    --no-abbrev, -A         Do not abbreviate text in tables. Default: false
    --table-style, -s <INTEGER>
                            Table style (0-11).
    --non-interactive, -n   Do not ask anything, use default answers automatically. Default: false
    --non-interactive-include-reboot-patches
                            Do not treat patches as interactive, which have the rebootSuggested-flag
                            set. Default: false
    --xmlout, -x            Switch to XML output.
    --ignore-unknown, -i    Ignore unknown packages. Default: false
    --terse, -t             Terse output for machine consumption. Implies --no-abbrev and
                            --no-color.


    --reposd-dir, -D <DIR>  Use alternative repository definition file directory.
    --cache-dir, -C <DIR>   Use alternative directory for all caches.
    --raw-cache-dir <DIR>   Use alternative raw meta-data cache directory.
    --solv-cache-dir <DIR>  Use alternative solv file cache directory.
    --pkg-cache-dir <DIR>   Use alternative package cache directory.

  Repository Options

    --no-gpg-checks         Ignore GPG check failures and continue. Default: false
    --gpg-auto-import-keys  Automatically trust and import new repository signing keys.
    --plus-repo, -p <URI>   Use an additional repository.
    --plus-content <TAG>    Additionally use disabled repositories providing a specific keyword. Try
                            '--plus-content debug' to enable repos indicating to provide debug
                            packages.
    --disable-repositories  Do not read meta-data from repositories.
    --no-refresh            Do not refresh the repositories.
    --no-cd                 Ignore CD/DVD repositories.
    --no-remote             Ignore remote repositories.
    --releasever            Set the value of $releasever in all .repo files (default: distribution
                            version)

  Target Options

    --root, -R <DIR>        Operate on a different root directory.
    --installroot <DIR>     Operate on a different root directory, but share repositories with the
                            host.
    --disable-system-resolvables
                            Do not read installed packages.

Commands:

      help, ?               Print zypper help
      shell, sh             Accept multiple commands at once.

  Repository Management:

      repos, lr             List all defined repositories.
      addrepo, ar           Add a new repository.
      removerepo, rr        Remove specified repository.
      renamerepo, nr        Rename specified repository.
      modifyrepo, mr        Modify specified repository.
      refresh, ref          Refresh all repositories.
      clean, cc             Clean local caches.

  Service Management:

      services, ls          List all defined services.
      addservice, as        Add a new service.
      modifyservice, ms     Modify specified service.
      removeservice, rs     Remove specified service.
      refresh-services, refs
                            Refresh all services.

  Software Management:

      install, in           Install packages.
      remove, rm            Remove packages.
      removeptf, rmptf      Remove (not only) PTFs.
      verify, ve            Verify integrity of package dependencies.
      source-install, si    Install source packages and their build dependencies.
      install-new-recommends, inr
                            Install newly added packages recommended by installed packages.

  Update Management:

      update, up            Update installed packages with newer versions.
      list-updates, lu      List available updates.
      patch                 Install needed patches.
      list-patches, lp      List available patches.
      dist-upgrade, dup     Perform a distribution upgrade.
      patch-check, pchk     Check for patches.

  Querying:

      search, se            Search for packages matching a pattern.
      info, if              Show full information for specified packages.
      patch-info            Show full information for specified patches.
      pattern-info          Show full information for specified patterns.
      product-info          Show full information for specified products.
      patches, pch          List all available patches.
      packages, pa          List all available packages.
      patterns, pt          List all available patterns.
      products, pd          List all available products.
      what-provides, wp     List packages providing specified capability.

  Package Locks:

      addlock, al           Add a package lock.
      removelock, rl        Remove a package lock.
      locks, ll             List current package locks.
      cleanlocks, cl        Remove useless locks.

  Locale Management:

      locales, lloc         List requested locales (languages codes).
      addlocale, aloc       Add locale(s) to requested locales.
      removelocale, rloc    Remove locale(s) from requested locales.

  Other Commands:

      versioncmp, vcmp      Compare two version strings.
      targetos, tos         Print the target operating system ID string.
      licenses              Print report about licenses and EULAs of installed packages.
      download              Download rpms specified on the commandline to a local directory.
      source-download       Download source rpms for all installed packages to a local directory.
      needs-rebooting       Check if the reboot-needed flag was set.
      ps                    List running processes which might still use files and libraries deleted
                            by recent upgrades.
      purge-kernels         Remove old kernels.

  Subcommands:

      subcommand            Lists available subcommands.

Type 'zypper help <COMMAND>' to get command-specific help.
```

# 𝗙𝗶𝗹𝗲 𝗩𝗶𝗲𝘄𝗶𝗻𝗴 𝗮𝗻𝗱 𝗘𝗱𝗶𝘁𝗶𝗻𝗴

## `cat`: Displays the contents of a file

```bash
⋊> ~ cat --help

Usage: cat [OPTION]... [FILE]...
Concatenate FILE(s) to standard output.

With no FILE, or when FILE is -, read standard input.

  -A, --show-all           equivalent to -vET
  -b, --number-nonblank    number nonempty output lines, overrides -n
  -e                       equivalent to -vE
  -E, --show-ends          display $ at end of each line
  -n, --number             number all output lines
  -s, --squeeze-blank      suppress repeated empty output lines
  -t                       equivalent to -vT
  -T, --show-tabs          display TAB characters as ^I
  -u                       (ignored)
  -v, --show-nonprinting   use ^ and M- notation, except for LFD and TAB
      --help        display this help and exit
      --version     output version information and exit

Examples:
  cat f - g  Output f\'s contents, then standard input, then g\'s contents.
  cat        Copy standard input to standard output.

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation <https://www.gnu.org/software/coreutils/cat>
or available locally via: info '(coreutils) cat invocation'
```

## `less`: Views the contents of a file with navigation capabilities

## `more`: Another file viewer with basic navigation

## `vim`: A powerful text editor with extensive features

## `nano`: A simple and user-friendly text editor for the terminal
