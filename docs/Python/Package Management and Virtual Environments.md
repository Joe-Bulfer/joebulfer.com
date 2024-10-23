### Overview 

There are many different ways to manage Python package versions and dependencies. Despite the Zen of Python saying "There should be only one obvious way to do it", Python itself is wide spread and used in many different domains, preferences and requirements start to develop across these many fields. System administrators often use the default package manager on their system (apt, yum, etc.) while those in the scientific community and data science use Anaconda, which bundles Python and R in it's own environments. The most common is to just use `pip`, the default package manager that grabs packages from PyPi (Python Package Index), in combination with Virtual Environment (`venv`), which is part of the standard library. `virtualenv` is a very similar tool which includes a few more features.

### Various Tools

Here are some various notes I've jotted down and other tools to be aware of.

Pipfile: the replacement for  pip's requirements.txt
`pipenv` combines pipfile, pip and `virtualenv`. 
`pyenv` isolates Python versions
`venv` is a built-in module in Python 3 while `virtualenv` is a third-party tool

This Stackoverflow [post](https://stackoverflow.com/questions/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe) sums everything up and is a great resource.

### venv and virtualenv 

venv is a subset of virtualenv integrated into the standard library which lacks the following features
- `app-data` seed method, which caches and speeds up the creation of virtual environments
- automatically discover python version to base virtual environment
- Support of Python 2
Despite being included in standard libraries of most distributions, on Debian/Ubuntu, it may not be and you'll have to `apt add-repository 'ppa:deadsnakes/ppa`, next `apt update`, then `sudo apt install python3.12-venv`
This [video](https://www.youtube.com/watch?v=MGTX5qI2Jts) is a good comparison between the two

For spinning up small projects, it seems `venv` is the best option as it is the standard library default and has less features (that's a good thing) than `virtualenv`.

To spin up a small project on Linux, run the following. The `-m` is for running library module as a script
```
python3 -m venv [project directory]
```
This will create a `bin` folder for executable files (possibly symlinks to host machine) including the Python interpreter, the very large `lib` folder which contains an entire copy of the Python standard library as well as any other package you install, the `include` directory for C headers to compile Python packages, and finally the `pyvenv.cfg` config file. 

To activate the environment, you can run the Bash script `bin/activate`. 
```
source `[project dir]/bin/activate`
```

Now anything you install with `pip3` will be confined to that environment, regardless of what directory you are in. Simply run `deactivate` when you are done.

### pipenv

Python is over a 30 year old language and some libraries have limitations and incompatibilities, [pipenv](https://github.com/pypa/pipenv) is a modern tool released in 2017 to bridge the gap between Pip, Python and virtualenv by having only a `pipfile` for package dependencies and `pipfile.lock` for version releases/builds and hashes as opposed to the antiquated `requirements.txt`. pipenv creates ands and manages virtualenv for you.
