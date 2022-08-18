# Django Cheat Sheet

## Creating Virtual Environments

### Create It

To create a virtual environment, decide upon a directory where you want to place it, and run the [`venv`](https://docs.python.org/3/library/venv.html#module-venv "venv: Creation of virtual environments.") module as a script with the directory path:

```
UNIX
python3 -m venv tutorial-env

WINDOWS
python -m venv tutorial-env
```

### Activate It

Once you’ve created a virtual environment, you may activate it.

```
On Windows, run:
tutorial-env\Scripts\activate.bat

On Unix or MacOS, run:
source tutorial-env/bin/activate
```

### Install Packages

After creating and activating your virtual environment, you can now install any external dependencies that you need for your project:

```
(venv) PS> python -m pip install <package-name>
```

`pip freeze` will produce a similar list of the installed packages, but the output uses the format that `pip install` expects. A common convention is to put this list in a `requirements.txt` file:

```
(tutorial-env) $ pip freeze > requirements.txt


(env) $ python -m pip install -r requirements.txt
```

### Deactivate

```
(venv) PS> deactivate
```

### Django project

```
(env) $ django-admin startproject <project-name>
```

void creating the additional top-level project folder

```
(env) $ django-admin startproject <projectname> .
```

### Django app

```
(env) $ python manage.py startapp <appname>
```

### Command Reference

![](C:\Users\Farid\AppData\Roaming\marktext\images\2022-07-26-18-09-39-image.png)

### Run Server

```
$ python manage.py runserver
$ python manage.py runserver 8080
$ python manage.py runserver 0:8080
```

Quit the server with CONTROL-C.

### Data Base / Model

```
py manage.py migrate

py manage.py makemigrations <app Name>

py manage.py sqlmigrate polls 001
```

Create SuperUser

```
python manage.py createsuperuser
```
