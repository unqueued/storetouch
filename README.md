# storetouch

This is a utility to take a snapshot of the modification times (mtimes) of files, and output a sequence of touch commands that can be used to restore their original state. It can be executed directly, or easily parsed.

The text before the first space is the command, the text before the second space is the timestamp, and then the filename is stored as an ansi-c literal and will work with any valid POSIX filename.

There are a myriad of similar tools like this. The closest inspiration is [git-store-meta](https://github.com/danny0838/git-store-meta), which stores more rich file metadata, but it relies directly on git, whereas this tools is completely portable.

There are plenty of cases where you may want to pin the mtimes of files where they are outside of git.

You may also be using git to use git to archive files and preserve their original timestamps, in a way which is not dependant on git itself.

I frequently use this for filesets alongside [git-annex](https://git-annex.branchable.com/), although git-annex has robust metadata ability itself and can automatically store the mtime in metadata, it is limited to files that are actually annexed, while storetouch does not rely on git at all, and will store the mtimes of any file or directory.

To make it more compatible with git-annex, it also uses the `-h` option to restore the mtime to broken symlinks, so you can use it against git-annex repos without their content being present. So that means you could clone a fileset without getting the binaries, restore the mtime to it's broken symlinks, make changes, and then regenerate and recommit.

Here are some examples of it's output from other repos:

```shell
touch -ht 198609180641.34 $'./Amanda Palmer & The Grand Theft Orchestr/Theatre Is Evil/02 Smile (Pictures or It Didn\'t Happ.mp3'
touch -ht 199602050810.38 $'./Amanda Palmer & The Grand Theft Orchestr/Theatre Is Evil/07 Trout Heart Replica.mp3'
touch -ht 200211131805.58 $'./The Damned/Singles/06 Is it a dream 2.mp3'
touch -ht 200211131811.50 $'./The Damned/Singles/08 Eloise 2.mp3'
touch -ht 200211131823.12 $'./The Damned/Singles/13 Gigolo 2.mp3'
touch -ht 200211131838.54 $'./The Damned/Singles/15 Alone Again or 2.mp3'
touch -ht 200211131855.04 $'./The Damned/Singles/01 Grimly Fiendish 1.mp3'
touch -ht 200211131855.04 $'./The Damned/Singles/01 Grimly Fiendish.mp3'
touch -ht 200211131857.02 $'./The Damned/Singles/02 Edward The Bear 1.mp3'
```

Via: [unqueued/ftp.rrc.pl_symbol-fileset](https://github.com/unqueued/ftp.rrc.pl_symbol-fileset)

```shell
touch -ht 200810021200.00 $'./Symbol/support_downloads/mobile computers/RemCapture'
touch -ht 200607101200.00 $'./Symbol/support_downloads/mobile computers/RemCapture/RemCapture v1.03.06-Release Notes.doc'
touch -ht 200806271200.00 $'./Symbol/support_downloads/mobile computers/RemCapture/Release Notes - RemCapture 1.05.02.htm'
touch -ht 200709041200.00 $'./Symbol/support_downloads/mobile computers/RemCapture/RemCapture-1.04.04.zip'
```

