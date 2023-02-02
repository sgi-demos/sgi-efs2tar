# efs2tar

`efs2tar` is a tool that converts SGI EFS-formatted filesystem images into tarballs. It was based entirely on NetBSD's `sys/fs/efs` ([source](http://cvsweb.netbsd.org/bsdweb.cgi/src/sys/fs/efs/?only_with_tag=MAIN)).

This fork auto generates .tar filenames if no -out parameter is provided, making it easier to run batch conversions, e.g. `find . -name "*.iso" -print -exec efs2tar -in {} ;\`.  The auto-generated tarball name is generated by replacing the source file's extension with `.tar`. If no extension is found on the source filename, then `.tar` is simply appended.  If the tarball already exists, no action is taken. 

## Example usage

```
$ go install github.com/sgi-demos/efs2tar
$ efs2tar -in ~/my-sgi-disc.iso
```

The Internet Archive has [several discs](https://archive.org/search.php?query=sgi&and%5B%5D=mediatype%3A%22software%22&page=2) in its collections that are formatted with EFS.


## "Edge cases" not covered
* any type of file other than directories and normal files (which is to say, links in particular do not work)
* partition layouts other than what you'd expect to see on an SGI-produced CDROM
* minimal error handling
* does not verify magic numbers
* preserving the original file permissions
* I've only tested this on like, one CD
