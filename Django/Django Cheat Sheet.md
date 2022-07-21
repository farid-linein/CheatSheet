# Django Cheat Sheet

## Creating Virtual Environments



To create a virtual environment, decide upon a directory where you want to place it, and run the [`venv`](https://docs.python.org/3/library/venv.html#module-venv "venv: Creation of virtual environments.") module as a script with the directory path:

```
UNIX
python3 -m venv tutorial-env

WINDOWS
python -m venv tutorial-env
```



Once you’ve created a virtual environment, you may activate it.

```
On Windows, run:
tutorial-env\Scripts\activate.bat

On Unix or MacOS, run:
source tutorial-env/bin/activate
```



`pip freeze` will produce a similar list of the installed packages, but the output uses the format that `pip install` expects. A common convention is to put this list in a `requirements.txt` file:

```
(tutorial-env) $ pip freeze > requirements.txt

```
