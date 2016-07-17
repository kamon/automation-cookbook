
# Installing Python on Mac

Python installation and setup on OS X for web development or scripting work.

## Python

Homebrew provides what they call a *formula* for Python 2.7.x and another one for Python 3.x.
They don't conflict, so they can both be installed. The resulting executable `python` will point to the 2.x
and `python3` to the 3.x version.

So, installing Python 2.7:

```
$ brew install python
...
==> Caveats
Pip and setuptools have been installed. To update them
  pip install --upgrade pip setuptools

You can install Python packages with
  pip install <package>

They will install into the site-package directory
  /usr/local/lib/python2.7/site-packages
...
```

Let's try it:

```
$ python
Python 2.7.11 (default, Dec  5 2015, 14:44:53)
[GCC 4.2.1 Compatible Apple LLVM 7.0.0 (clang-700.1.76)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

And installing Python 3 is done the same way, except we point to `python3`:

```
$ brew install python3
...
==> Summary
🍺  /usr/local/Cellar/python3/3.5.1: 3420 files, 59M
```

Run `python3` to use it:

```
$ python3
Python 3.5.1 (default, Dec  7 2015, 21:59:10)
[GCC 4.2.1 Compatible Apple LLVM 7.0.0 (clang-700.1.76)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

## Using virtual Python environments

The [virtualenv](http://virtualenv.readthedocs.org/en/latest/) tool helps create isolated Python environments.
Basically, you use it to create a folder that will contain all the executables and libraries that a specific Python project needs. You will be able to run Python inside that folder and install your project's dependencies (generally using `Pip`) in an isolated way, i.e. without interfering with another project which has its own "virtual env".

Check the website for all you need to get started with `virtualenv`.

First, let's install it on our previously Homebrew-installed Python 2.7:

```
$ pip install virtualenv
```

Note that we are actually calling `/usr/local/Cellar/python/2.7.11/bin/pip` since Python was installed under
`/usr/local/Cellar/python`.

To ease my work, I will also use the [virtualenvwrapper](http://virtualenvwrapper.readthedocs.org/en/latest/) package, which provides a set of productivity commands for working with virtual environments.

Install it:

```
$ pip install virtualenvwrapper
```

Let's make sure my environments are placed in my home under `~/.virtualenvs`:

```
$ export WORKON_HOME=~/.virtualenvs
```

Then we need to override the `$PATH` search by setting `VIRTUALENVWRAPPER_PYTHON` to the full path of the Python interpreter to use, and `VIRTUALENVWRAPPER_VIRTUALENV` to the full path of the "virtualenv" binary to use.

```
$ export VIRTUALENVWRAPPER_PYTHON=/usr/local/Cellar/python/2.7.11/bin/python
$ export VIRTUALENVWRAPPER_VIRTUALENV=/usr/local/bin/virtualenv
```

Then use the `source` command to source `virtualenvwrapper`'s shell script (installed under `/usr/local/bin`
in my case) to your shell startup file:

```
$ source /usr/local/bin/virtualenvwrapper.sh
```

After that, let's say we need to create a new isolated environment to be used for working with Plone 5.
It's quick and easy using the `mkvirtualenv` command:

```
$ mkvirtualenv env-plone5

New python executable in env-plone5/bin/python2.7
Also creating executable in env-plone5/bin/python
Installing setuptools, pip, wheel...done.
virtualenvwrapper.user_scripts creating /Users/kayeva/.virtualenvs/env-plone5/bin/predeactivate
virtualenvwrapper.user_scripts creating /Users/kayeva/.virtualenvs/env-plone5/bin/postdeactivate
virtualenvwrapper.user_scripts creating /Users/kayeva/.virtualenvs/env-plone5/bin/preactivate
virtualenvwrapper.user_scripts creating /Users/kayeva/.virtualenvs/env-plone5/bin/postactivate
virtualenvwrapper.user_scripts creating /Users/kayeva/.virtualenvs/env-plone5/bin/get_env_details
(env-plone5)$
```

After you have finished and want to stop working on the environment, just type `deactivate`:

```
(env-plone5)$ deactivate
$
```

To see how `virtualenvwrapper`'s `workon` command allows us to interact with "virtual envs" we have created, here are two examples:

```
$ workon
env-mrbob
env-plone5
env-redislite
```

```
$ workon env-mrbob
(env-mrbob)$
(env-mrbob)$ ...
(env-mrbob)$ workon env-plone5
(env-plone5)$
```

