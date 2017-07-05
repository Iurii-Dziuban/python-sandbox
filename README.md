Anaconda, python and pip Quick practical guide
================================================
Table of contents:
 * [Anaconda, python, pip. Quick practical guide](#anaconda,-python-and-pip-quick-practical-guide)

## Download
Download anaconda from https://www.continuum.io/downloads for windows/mac/linux with python2/python3

## Install
Follow the instructions and install it.

### Check "conda" and "python" are accessible from the command line:
```
conda --help
conda --version
conda list
python --version
```
### Update anaconda to latest version:

```conda update conda```

## Environments 

### Create environment

```
conda create -n [env_name] python=[python_version]
```
Examples:
```
conda create --name python2 pip
conda create --name python3 python=3.6
```
* python2, python3 - names of environments that are created by default in the envs directory in your conda directory
* pip - package to be installed to the env. You can specify as many packages as you need in the end of command line, separated by space
* python= - gives possibility to specify python version to be used as a default in the env

### List envs
`conda info --envs`

### Activate/Deactivate environment
```source activate [env_name]``` (Linux) 
and ```activate [env_name]``` (Windows)
Example: `source activate python3` and `activate python3`

Check that packages are from the activated env:
Examples: 
```
python --version
pip --version
```

to deactivate `deactivate`

### Make exact copy of the env

```
conda create --name <new env name> --clone <existing env name>
```
Example: 
```
conda create --name python3copy --clone python3
```

### Delete env completely

```
conda remove --name <env name> --all
```
Example: 
```
conda remove --name python3 --all
```

### List env packages installed
```
conda list
```

### Export current env to file

```
conda list --explicit > <filename>
```
Example: 
```
conda list --explicit > DEV/env.txt
```

### Create own env file
Example: file 
```
environment.yaml
```
Content:
```
name: stats
dependencies:
  - numpy
  - pandas
  - python=3.6
  - pip:
    - Flask-Testing
```	
### Import env from file 
```
conda create --name <env> --file <filename>
```
Example 
```
conda create --name python3new --file environment.yaml
```

### Windows: Activate/Deactivate ENV variables for the env
```
cd <anaconda folder>/envs/<env name>
mkdir .\etc\conda\activate.d
mkdir .\etc\conda\deactivate.d
type NUL > .\etc\conda\activate.d\env_vars.bat
type NUL > .\etc\conda\deactivate.d\env_vars.bat
```
Edit `.\etc\conda\activate.d\env_vars.bat`

```
set MY_ANACONDA_TEST='Hello World'
```

Edit `.\etc\conda\deactivate.d\env_vars.bat`

```
set MY_ANACONDA_TEST=
```

Check it works on activate/deactivate the environment

### Linux/Mac: Activate/Deactivate ENV variables for the env

```
cd <anaconda folder>/envs/<env name>
mkdir -p ./etc/conda/activate.d
mkdir -p ./etc/conda/deactivate.d
touch ./etc/conda/activate.d/env_vars.sh
touch ./etc/conda/deactivate.d/env_vars.sh
```
Edit `./etc/conda/activate.d/env_vars.sh`

```
 #!/bin/sh

 export MY_ANACONDA_TEST='Hello World'
```

Edit `./etc/conda/deactivate.d/env_vars.sh`

```
 #!/bin/sh

 unset MY_ANACONDA_TEST
```

Check it works on activate/deactivate the environment

## Packages

### Search for package versions
```
conda search --full-name <package name>
```
Example: 
```
conda search --full-name python
```

### Install package to active env
```
conda install <package name>
``` 
or
```
conda install <package name> = <package version>
```
Example: 
```
conda install pip
``` 
or 
```
conda install pip=9.0.1
```


Check pip location: **(Mac/Linux)**: `which -a pip`  **(Windows)**: `where pip`
Check python location: **(Mac/Linux)**: `which -a python`  **(Windows)**: `where python`
**Only if you activated env!** otherwise it will be install to different directory :

Remote file
```
pip install <package>
``` 

Local file:
```
pip install relative_path_to_seaborn.tar.gz
```
Or 
```
pip install .
```
Or
```
python setup.py install
```

### Update package to new version

```
conda update <package name>
``` 
or 
```
pip install --upgrade <package name>
```

Example: `conda update pip`

### Remove package
```
conda remove <package name>
```
Example:
```
conda remove pip
```
## Revisions
Conda tracks changes in the libraries via revisions

### List revisions
```
conda list --revisions
```

### Install specific revision
```
conda install --revision 2
```

## Creating/Distributing/Using own packages

### Create own package

```
conda metapackage custom-r-bundle 0.1.0 --dependencies r-irkernel jupyter r-ggplot2 r-dplyr --summary "My custom R bundle" 
```

### Upload own package
```
conda install anaconda-client
anaconda login
anaconda upload path/to/custom-bundle-0.1.0-0.tar.bz2
```

### Use own package

```
conda install -c <your anaconda.org username> custom-bundle
```

# Remove anaconda
`rm -rf <anaconda install directory>`
Example: `rm -rf ~/anaconda` 
On Windows remove from the installed programs.
Example `rmdir /s anaconda`

# Other languages. Like R
```
conda install -c r r-essentials
conda update -c r r-essentials
```
# !!!!!!!!!! PyCharm !!!!!!!!!!!!!!!!!!!!!!



# !!!!!!!!!! Pybuilder !!!!!!!!!!!!!!!!!!!!

## Urls
- http://pybuilder.github.io/
- Basic Tutorial: http://pybuilder.github.io/documentation/tutorial.html
- List of available plugins: http://pybuilder.github.io/documentation/plugins.html
- Project examples using PyBuilder: http://pybuilder.github.io/documentation/examples.html

## Install
`pip install pybuilder`

## Create new project

*NOTE!!!* for Windows use command *`pyb_`* instead of `pyb`
Installing dependecies and building with default goal
```
pyb --start-project
pyb install_dependencies publish
pyb
```
## Existing project
```
pyb install_dependencies
pyb
```

## Describing available tasks
`pyb -t`

## Providing parameters
`pyb -P spam="spam message"`

## IDE integration

### PyCharm (Intellij IDEA)
build.py: `use_plugin('python.pycharm')`
Command line: `pyb pycharm_generate`

### PyDev (Eclipse)
build.py: `use_plugin('python.pydev')`
Command line: `pyb pydev_generate`
