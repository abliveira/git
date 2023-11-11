## gitignore

Create a file '.gitignore'

Ignored Files
- Ignored files are invisible to git
- Each directory may contain a file named .gitignore which lists either specific files or
name patterns which are to be ignored
- For instance many temporary files could be ignored with a specification like *.o
- The .gitignore file in any directory applies recursively to all subdirectories below it,
so if you specify a filename or pattern in the main directory, all files fitting the
description will be invisible

It is also possible to override the rules by prefixing with !; for example, if your
.gitignore file includes:
*.ko
!my_driver.ko
- The second specification overrides the first more general one, and the file
my_driver.ko will be tracked

Comments in gitignore can be done using # at the start of a line

There can be .gitignore files in each subdirectory, with rules applying recursively and thus incrementally