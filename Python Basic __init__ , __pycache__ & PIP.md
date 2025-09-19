## Why we need __init__? 


#### 1. Purpose of __init__.py

- __init__.py file in a directory tells Python that the directory should be treated as a package.
- This allows you to import modules from that directory using package syntax, e.g.:
- Without __init__.py, Python (pre-3.3) would not recognize the folder as a package, and imports might fail.
- The file can be empty, or it can contain initialization code for the package.


Starting with Python 3.3 and above (including Python 3.11), you can technically remove the __init__.py file from a package directory, and Python will still recognize it as a package due to "implicit namespace packages."

#### However, you should keep __init__.py:

- When you add an __init__.py file to a package directory, it does not create a global namespace. Instead, it defines a package namespace.

- All modules and submodules inside that package share the package’s namespace (e.g., tools_package.audio.utils).
- This keeps your package’s contents organized and separate from the global namespace, preventing naming conflicts.

#### Module vs Package

- Module: A single Python file (e.g., utils.py). You import it like import utils or from utils import foo.

- Package: A directory containing an __init__.py file and (usually) multiple modules (e.g., audio/ with __init__.py and utils.py).



## 2. What is __pycache__?

- When you run or import Python code, Python compiles .py files to bytecode for faster execution.

- The compiled bytecode files are stored in the __pycache__ directory, with names like utils.cpython-311.pyc.
- **cpython-311** means the file was compiled by CPython version 3.11.
- These .pyc files are used by Python to speed up future imports of the module.


## 3. PIP (pip installs packages) (package Manager for Python):-


#### Using pip in a Python Virtual Environment

``` python
$ python -m venv venv/
$ source venv/bin/activate

(venv) $ pip3 --version
pip 24.2 from .../python3.12/site-packages/pip (python 3.12)

(venv) $ pip --version
pip 24.2 from .../python3.12/site-packages/pip (python 3.12)
```

- Here you initialize a virtual environment named venv by using Python’s built-in venv module. 
- After running the command above, Python creates a directory named venv/ in your current working directory. 
- Then, you activate the virtual environment with the source command. - The parentheses (()) surrounding your venv name indicate that you successfully activated the virtual environment.

- Finally, you check the version of the pip3 and pip executables inside your activated virtual environment.
- Both point to the same pip module, so once your virtual environment is activated, you can use either pip or pip3.


#### Installing Packages With pip

```python
 install a package
       pip install package_name
 uninstall a package
       pip uninstall package_name
 list installed packages
       pip list
 install a specific version of a package
       pip install package_name==version_number
 upgrade a package
       pip install --upgrade package_name
 show package information
       pip show package_name
 search for packages
       pip search package_name
```

### Using Requirements Files

```python
 requirement.text package
       pip install -r requirements.txt
 make a requirements.txt file from the packages installed
       pip freeze > requirements.txt
```

certifi==x.y.z
charset-normalizer==x.y.z
idna==x.y.z
**requests>=x.y.z, <3.0**
urllib3==x.y.z

Changing the version specifier for the requests package ensures that any version greater than or equal to 3.0 doesn’t get installed.


#### very important 
We can create 3 files

- requirements_dev.txt (For Development)
- requirements_prod.txt (For Production)
- requirements_lock.txt (After Development complete --> We will freeze it)

### Uninstalling Packages With pip

```python
pip show <package Name>
```

Name: requests
Version: 2.32.3
Summary: Python HTTP for Humans.
Location: .../python3.12/site-packages
**Requires: certifi, idna, charset-normalizer, urllib3
Required-by:**

- Notice the last two fields, Requires and Required-by. The show command tells you that requests requires certifi, idna, charset-normalizer, and urllib3. You probably want to uninstall those too. Notice that requests isn’t required by any other package.
- So it’s safe to uninstall it.

```python
pip uninstall certifi urllib3 -y
```

Here you uninstall urllib3. Using the -y switch, you suppress the confirmation dialog asking you if you want to uninstall this package.

In a single call, you can specify all the packages that you want to uninstall
