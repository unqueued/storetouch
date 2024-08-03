# storetouch

This is a utility to take a snapshot of the modification times (mtimes) of files, and output a sequence of touch commands that can be used to restore their original state. It can be executed directly, or easily parsed.

The text before the first space is the command, the text before the second space is the timestamp, and then the filename is stored as an ansi-c literal and will work with any valid POSIX filename:

```shell
touch -ht 202408031357.23 $'.'
touch -ht 202110281139.03 $'./storetouch'
touch -ht 202408031357.23 $'./README.md'
```

There are a myriad of similar tools like this. The closest inspiration is [git-store-meta](https://github.com/danny0838/git-store-meta), which stores more rich file metadata, but it relies directly on git, whereas this tools is completely portable.

There are plenty of cases where you may want to pin the mtimes of files where they are outside of git.

You may also be using git to use git to archive files and preserve their original timestamps, in a way which is not dependant on git itself.

I frequently use this for filesets alongside [git-annex](https://git-annex.branchable.com/), although git-annex has robust metadata ability itself and can automatically store the mtime in metadata, it is limited to files that are actually annexed, while storetouch does not rely on git at all.

To make it more compatible with git-annex, it also uses the `-h` option to restore the mtime to broken symlinks, so you can use it against git-annex repos without their content being present.
