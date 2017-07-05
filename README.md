Anaconda, python and pip Quick practical guide
================================================
Table of contents:
 * [Anaconda, python, pip. Quick practical guide](#anaconda-python-and-pip-quick-practical-guide)
   * [Download](#download-anaconda)
   * [Install](#install-anaconda)
   * [Environments](#anaconda-environments)
   * [Packages](#anaconda-packages)
   * [Own packages](#own-packages)
   * [Remove anaconda](#remove-anaconda)
   * [Other languages](#other-languages)
   * [Projects](#projects)
 * [PyCharm configuration](#pycharm)
 * [PyBuilder configuration](#pybuilder)
   * [Urls](#pybuilder-urls)
   * [Install](#install-pybuilder)
   * [Create new project](#create-new-project)
   * [Existing project](#existing-project)
   * [Describing available tasks](#describing-available-tasks)
   * [Providing parameters](#providing-parameters)
   * [IDE integration](#ide-integration)

Download anaconda
-----------------
Download anaconda from https://www.continuum.io/downloads for windows/mac/linux with python2/python3

Install anaconda
----------------
Follow the instructions and install it.

### Check "conda" and "python" are accessible from the command line:
```bash
conda --help
conda --version
conda list
python --version
```
### Update anaconda to latest version:

```bash
conda update conda
```

Anaconda Environments 
---------------------
### Create environment

```bash
conda create -n [env_name] python=[python_version]
```
Examples:
```bash
conda create --name python2 pip
conda create --name python3 python=3.6
```
* python2, python3 - names of environments that are created by default in the envs directory in your conda directory
* pip - package to be installed to the env. You can specify as many packages as you need in the end of command line, separated by space
* python= - gives possibility to specify python version to be used as a default in the env

### List envs
`conda info --envs`

### Activate/Deactivate environment
```
source activate [env_name]
``` 
**(Linux)**
and 
```
activate [env_name]
``` 
**(Windows)**
Example: `source activate python3` and `activate python3`

Check that packages are from the activated env:
Examples: 
```bash
python --version
pip --version
```

to deactivate `deactivate`

### Make exact copy of the env

```bash
conda create --name <new env name> --clone <existing env name>
```
Example: 
```bash
conda create --name python3copy --clone python3
```

### Delete env completely

```bash
conda remove --name <env name> --all
```
Example: 
```bash
conda remove --name python3 --all
```

### List env packages installed
```bash
conda list
```

### Export current env to file

```bash
conda list --explicit > <filename>
```
Example: 
```bash
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
```bash
conda create --name <env> --file <filename>
```
Example 
```bash
conda create --name python3new --file environment.yaml
```

### Windows: Activate/Deactivate ENV variables for the env
```bash
cd <anaconda folder>/envs/<env name>
mkdir .\etc\conda\activate.d
mkdir .\etc\conda\deactivate.d
type NUL > .\etc\conda\activate.d\env_vars.bat
type NUL > .\etc\conda\deactivate.d\env_vars.bat
```
Edit `.\etc\conda\activate.d\env_vars.bat`

```bash
set MY_ANACONDA_TEST='Hello World'
```

Edit `.\etc\conda\deactivate.d\env_vars.bat`

```bash
set MY_ANACONDA_TEST=
```

Check it works on activate/deactivate the environment

### Linux/Mac: Activate/Deactivate ENV variables for the env

```bash
cd <anaconda folder>/envs/<env name>
mkdir -p ./etc/conda/activate.d
mkdir -p ./etc/conda/deactivate.d
touch ./etc/conda/activate.d/env_vars.sh
touch ./etc/conda/deactivate.d/env_vars.sh
```
Edit `./etc/conda/activate.d/env_vars.sh`

```bash
 #!/bin/sh

 export MY_ANACONDA_TEST='Hello World'
```

Edit `./etc/conda/deactivate.d/env_vars.sh`

```bash
#!/bin/sh

unset MY_ANACONDA_TEST
```

Check it works on activate/deactivate the environment

Anaconda Packages
-----------------
### Search for package versions
```bash
conda search --full-name <package name>
```
Example: 
```bash
conda search --full-name python
```

### Install package to active env
```bash
conda install <package name>
``` 
or
```bash
conda install <package name> = <package version>
```
Example: 
```bash
conda install pip
``` 
or 
```bash
conda install pip=9.0.1
```
Check pip location: **(Mac/Linux)**: `which -a pip`  **(Windows)**: `where pip`
Check python location: **(Mac/Linux)**: `which -a python`  **(Windows)**: `where python`
**Only if you activated env!** otherwise it will be install to different directory :

Remote file
```bash
pip install <package>
``` 

Local file:
```bash
pip install relative_path_to_seaborn.tar.gz
```
Or 
```bash
pip install .
```
Or
```bash
python setup.py install
```

### Update package to new version

```bash
conda update <package name>
``` 
or 
```bash
pip install --upgrade <package name>
```

Example: `conda update pip`

### Remove package
```bash
conda remove <package name>
```
Example:
```
conda remove pip
```bash
## Revisions
Conda tracks changes in the libraries via revisions

### List revisions
```bash
conda list --revisions
```

### Install specific revision
```bash
conda install --revision 2
```

Own packages
------------

### Create own package

```bash
conda metapackage custom-r-bundle 0.1.0 --dependencies r-irkernel jupyter r-ggplot2 r-dplyr --summary "My custom R bundle" 
```

### Upload own package
```bash
conda install anaconda-client
anaconda login
anaconda upload path/to/custom-bundle-0.1.0-0.tar.bz2
```

### Use own package

```bash
conda install -c <your anaconda.org username> custom-bundle
```

Remove anaconda
---------------
`rm -rf <anaconda install directory>`
Example: `rm -rf ~/anaconda` 
On Windows remove from the installed programs.
Example `rmdir /s anaconda`

Other languages
---------------
Like R
```bash
conda install -c r r-essentials
conda update -c r r-essentials
```

Projects
--------
### Create requirements.txt

```bash
pip install pipreqs
pipreqs /path/to/project
```
**Note** Works for pybuilder project

PyCharm
=======


PyBuilder
=========
PyBuilder Urls
--------------
- http://pybuilder.github.io/
- Basic Tutorial: http://pybuilder.github.io/documentation/tutorial.html
- List of available plugins: http://pybuilder.github.io/documentation/plugins.html
- Project examples using PyBuilder: http://pybuilder.github.io/documentation/examples.html

Install PyBuilder
-----------------
`pip install pybuilder`

Create new project
------------------

**NOTE!!!** for Windows use command **`pyb_`** instead of `pyb`
Installing dependencies and building with default goal
```
pyb --start-project
pyb install_dependencies publish
pyb
```
Existing project
----------------
```
pyb install_dependencies
pyb
```

Describing available tasks
--------------------------
```
pyb -t
```

Providing parameters
--------------------
```
pyb -P spam="spam message"
```

IDE integration
---------------
### PyCharm (Intellij IDEA)
build.py: `use_plugin('python.pycharm')`
Command line: `pyb pycharm_generate`

### PyDev (Eclipse)
build.py: 
```
use_plugin('python.pydev')
```
Command line: 
```
pyb pydev_generate
```
