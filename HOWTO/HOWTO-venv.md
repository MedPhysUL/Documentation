# HOWTO - venv

## Introduction

Creating a virtual environment allows the user to have a desired version of python or have installed packages that are independent of the general version installed on the computer. As the name implies, this creates a new environment for the code to run outside the general system. 
This can be especially useful when running or creating code that requires specific versions of some packages and that one does not wish to uninstall and reinstall python and the necessary packages. 

## Prerequisites

 * Python 3
   * Although there are many sources from which one may download python, it is usually downloaded from the [python website](https://www.python.org/downloads/).
 * Pip
   * Pip is most likely already installed with python, if it is not then it can be installed with the command ```python -m ensurepip --upgrade```. For Mac users, replacing _python_ with _python3_ is recommended to ensure that the command does not refer to python 2.
 * virtualenv 
   * This is a required python package that allows the creation of virtual environments. It is usually pre-installed with python, but if it is not it can ben manually installed with ```pip install virtualenv```. For Mac users, replacing _pip_ with _pip3_ is recommended to ensure that the command does not refer to python 2.

## 1. Set-up

### Creating a virtual environment on Windows 

1. Open a terminal in the desired root repository:
   1. Open the desired root repository in the file manager.
   2. Click on the path to the repository, write 'cmd' and press enter to open the terminal at the location.`

2. Create the virtual environment:
   1. Write in the command line ```python -m virtualenv name_of_the_virtual_environment``` with "name_of_the_virtual_environment" replaced with the desired name of the virtual environment, usually venv. For simplicity, the name of the virtual environment will now be considered to be venv.

3. Activate the virtual environment:
   1. Write in the same terminal ```cd  venv/Scripts/activate``` to activate the virtual environment.
   2. When in a terminal at the virtual environment location, "(venv)" should appear at the left of the command line.

### Creating a virtual environment on Mac OS

1. Open a terminal in the desired root repository:  
   1. Find the desired root repository in Finder.
   2. Right-click on the repository and select "New Terminal at Folder" at the bottom of the options.

2. Create the virtual environment:
   1.  Write the ```python3 -m virtualenv venv``` command in the terminal.

3. Activate the virtual environment:
   1. Write in the same terminal ```source venv/bin/activate``` to activate the virtual environment.
   2.  When in a terminal at the virtual environment location, "(venv)" should appear at the left of the command line.

## 2. Using the virtual environment as the python interpreter for an IDE

### PyCharm

1. Press "cmd + ," on Mac or "ctrl + ," on Windows.
2. Go in "Project: Documentation" -> "Python Interpreter".
3. Click on "Add Interpreter" - > "Add Local Interpreter".
4. In "Virtualenv Environment" Select "Existing".
5. Click on the "..." and find the virtual environment repository.
6. Within the repository, find the desired python version and select it. 
7. Although this might require a new terminal window, the PyCharm terminal should now also have its command lines start with "(venv)".
8. From now on, any package installed from the PyCharm terminal will be installed in the virtual environment rather than the general environment.

### VSCode

1. Press "cmd + shift + P" on Mac or "ctrl + shift + P" on Windows to open a search bar.
2. Find and choose "Python: Select Interpreter" -> "Enter Interpreter Path".
3. Find the virtual environment repository.
4. Within the repository, find the desired python version and select it. 
5. Although this might require a new terminal window, the VSCode terminal should now also have its command lines start with "(venv)".
6. From now on, any package installed from the VSCode terminal will be installed in the virtual environment rather than the general environment.

## Conclusion

Most steps are straightforward, but if need be, here are some sources that can help (arranged in no particular order):

General:
- [venv python documentation](https://docs.python.org/3/library/venv.html)
- [Using multiple venvs](https://sparkbyexamples.com/python/using-different-python-versions-with-virtualenv/?expand_article=1)

Mac OS:
- [venv on Mac](https://www.studytonight.com/post/python-virtual-environment-setup-on-mac-osx-easiest-way)
- [venv on Mac](https://mnzel.medium.com/how-to-activate-python-venv-on-a-mac-a8fa1c3cb511)
- [venv on Mac](https://sourabhbajaj.com/mac-setup/Python/virtualenv.html)
- [venv on Mac](https://programwithus.com/learn/python/pip-virtualenv-mac)

Windows:
- [venv on Windows 10](https://www.liquidweb.com/kb/how-to-setup-a-python-virtual-environment-on-windows-10/)
- [venv on Windows](https://programwithus.com/learn/python/pip-virtualenv-windows)
- [venv on Windows from scratch](https://linuxhint.com/activate-virtualenv-windows/)

IDE:
- [VSCode venv setup](https://code.visualstudio.com/docs/python/environments)
- [Pycharm venv setup](https://www.jetbrains.com/help/pycharm/creating-virtual-environment.html#python_create_virtual_env)
