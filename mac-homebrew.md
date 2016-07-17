I had to reinstall all my tools on a new Mac, and I took the opportunity to do things in ways
that allow more productivity. Hopefully, I would also avoid situations where things break with future
software installs or updates.

Here are my quick notes on the process. In part 1, I am covering the first requirements to get running for some of my development tasks: *Git*, *Ruby*, and the OS X package manager *Homebrew*. Part 2 will be dedicated to *Python*, which I use a lot.  

Actually, Git and Ruby were already installed on that system, OS X El Capitan, so I had less to do.
The only additional requirement was *XCode*, which was easy to install, so I will skip that part.

## Homebrew

Following the recommended installation method, using the Ruby command
`ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`,
I got the following output:

```
==> This script will install:
/usr/local/bin/brew
/usr/local/Library/...
/usr/local/share/man/man1/brew.1
==> The following directories will be made group writable:
/usr/local/.
/usr/local/bin
/usr/local/etc
/usr/local/lib
/usr/local/share
/usr/local/share/man
/usr/local/share/man/man1
/usr/local/share/doc
==> The following directories will have their owner set to ...:
/usr/local/.
/usr/local/bin
/usr/local/etc
/usr/local/lib
/usr/local/share
/usr/local/share/man
/usr/local/share/man/man1
/usr/local/share/doc
==> The following directories will have their group set to admin:
/usr/local/.
/usr/local/bin
/usr/local/etc
/usr/local/lib
/usr/local/share
/usr/local/share/man
/usr/local/share/man/man1
/usr/local/share/doc

Press RETURN to continue or any other key to abort
...
...
==> Downloading and installing Homebrew...
remote: Counting objects: 3902, done.
remote: Compressing objects: 100% (3746/3746), done.
remote: Total 3902 (delta 31), reused 2341 (delta 19), pack-reused 0
Receiving objects: 100% (3902/3902), 3.39 MiB | 841.00 KiB/s, done.
Resolving deltas: 100% (31/31), done.
From https://github.com/Homebrew/homebrew
 * [new branch]      master     -> origin/master
HEAD is now at 567bff2 cless: tweak formula
==> Installation successful!
==> Next steps
Run `brew help` to get started
```

Then installing a software package is done with the `brew` command.
For example, for installing Python: `brew install python`.
But we'll see that in detail in the next part of this several parts article.

## Cask

In addition to Homebrew, I am using [Cask](http://caskroom.io/) for easily installing *everyday* applications,
as long as they have been packaged for Cask.

Citing the project's website is the best way to introduce Cask:

<blockquote>
Homebrew Cask extends Homebrew and brings its elegance, simplicity, and speed to OS X applications and large binaries alike.
<br>
It only takes 1 line in your shell to reach 2940 Casks maintained by 433 contributors.
</blockquote>

The available packages, called *Casks*, can be found via the search interface at [http://caskroom.io/search](http://caskroom.io/search).
Installing Cask itself is done using Homebrew. Check the documentation on the site for more.

Here are examples showing how to install common applications or software tools:
* `brew cask install google-chrome`
* `brew cask install textwrangler`
* `brew cask install vlc`
* `brew cask install maxthon`
* `brew cask install flux`
