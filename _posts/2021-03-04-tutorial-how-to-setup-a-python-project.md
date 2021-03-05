---
layout: post
title:  "Tutorial: How to setup a python project"
permalink: /tutorials/how-to-setup-a-python-project
tags: tutorial python intellij git gitignore logging config annotations virtualenv folder-structure testing
---

In this tutorial we show how to set up a python project in Intellij from scratch.
The reader will be provided with a project structure which covers many basic topics that are essential in a professional software project, like git, virtual environments, logging, configuration and testing.
Our second focus is on how to configure and run the project in Intellij.

[See here for the GitHub repository corresponding to this tutorial.](https://github.com/zoowirt/python-project-setup-tutorial)


## Prerequisites
* Python 3.7 or higher
* Intellij Community or Professional (Version 2020.3 works fine)
* git
* (optional) an account on github, gitlab, or similar


## Initializing a new git repository

This first part is optional, but using git as version control is highly recommended. In case you do not want to use a remote git server, just create a folder on your locale machine that contains a file named `README.md`. Then navigate in Intellij to `File > Open` and open the project. In the tutorial, continue with [The folder structure of the repository](#the-folder-structure-of-the-repository).

### Creating a repository on github.com
On [github.com](https://github.com/) (or similar), create a new repository, and initialize it with a `README` file. Do *not* add a `.gitignore` file, as we will do this manually later.

![](/images/tutorial-how-to-setup-a-python-project/add_readme_file.png)

### Cloning the repository to your local machine
On the repository's github page, navigate to `Code` and copy the  `HTTPS` url.

![](/images/tutorial-how-to-setup-a-python-project/copy_git_clone_url.png)

Open a terminal, go to the folder where you want the repo to have and execute the following (replacing the url by the one of your repo):

`git clone https://github.com/zoowirt/python-project-setup-tutorial.git`

Now the repository exists on your local machine. At the moment it only contains the `README.md` file.

**Remark:** In practice it is convenient to have all repositories organized in one folder (and subfolders thereof). This folder is often called `workspace` or `workbench`.

### Opening the project in Intellij
In Intellij, navigate to `File > Open` and open the project.

### Creating a `.gitignore` file
There will be files and folders on your local machine that you do not want to add to the git repository. For instance, Intellij creates a folder `.idea` to record the local IDE settings. It causes a big mess if these files are not ignored, since other people working on the project will have other settings, which leads to merge conflicts.

A file named `.gitignore` in the root folder tells git what to ignore. It is quite convenient to use an automatic creator of a `.gitignore` file, e.g., [gitignore.io](https://www.toptal.com/developers/gitignore). The generation of the file is based on key words for the technology for the project. For a basic python project in Intellij, the key words `python` and `intellij+all` are sufficient.

![](/images/tutorial-how-to-setup-a-python-project/gitignore.png)

After hitting the `Create` button, the content of the gitignore file is shown as plain text in the browser. In the repository's root folder, create a file named `.gitignore` and copy the plain text there. Add the file to git as Intellij automatically asks you to:

![](/images/tutorial-how-to-setup-a-python-project/adding_gitignore.png)

One can manually add further folders or files to `.gitignore`. Alternatively, in Intellij one can add a file to `.gitignore` by right-clicking and navigating to `Git > Add to .gitignore`.

### The git status of files

Intellij indicates the present git status of each file in the repository by means of colors.

* black: file is versioned and has not been changed since the last commit
* red: file is unversioned
* green: file is added, but not commited
* blue: file is commited, but has been changed since the last commit
* grey: file is ignored

![](/images/tutorial-how-to-setup-a-python-project/git_status.png)

Every time a file is created in Intellij, one is asked to add the file to git (see above). If a file is created from outside Intellij (e.g., by copying it manually to the repository), it is unversioned (red) by default. To add the file to git in Intellij, right-click the file and click `Git > Add`.

### git pull, commit and push in Intellij

Intellij has a convenient graphical user interface for git included. It can be found in the main menu bar, as well as in the right upper bar:

![](/images/tutorial-how-to-setup-a-python-project/git_menu_bar.png)

The buttons mean git pull, git commit and git push, respectively. For instance, after clicking the commit button, a nice menu opens up which displays the changes made since the last commit. The interface for solving merge conflicts is also worth mentioning. If the Intellij git features are not sufficient, one can still use a terminal.

## The folder structure of the repository

In practice there is a more or less standard folder structure for python projects, which is also supported by Intellij.

* `src`: working directory and folder for the productive source code. It does *not* contain any kind of tests, deployment configuration or documentation.
* `src/main.py`: the entrypoint for the project.
* `src/util`: folder for util code, e.g., for handling config files.
* `test`: folder for the test code. The test code is strictly separeted from the productive source code.
* `doc`: folder for files supplementing the `README` file (if such files exists). In this sample project we collect the screens

It is convenient mark the `src` and `test` folder as such in Intellij. To do so, navigate to `File > Project Structure` and then on the left to `Project Settings > Modules`. Mark the folders accordingly, click `Apply` and then `OK`.

![](/images/tutorial-how-to-setup-a-python-project/marking_sources.png)

## Setting up a python virtual environment

There are many good reasons to create an individual virtual environment for each software project - even though it seems highly redundant at first glance. It is in fact a very bad idea to run each project in the same environment.
* As python and modules evolve, incompatiblities occur. It might happen that one project necessarily requires another version than another project.
* The environment on your local machine, where the code is written, should be identical to the one used in a productive system. This is guarenteed by fixing the precise environment and versions of modules.
* If updates of libraries become necessary, e.g., because of security pathces, the updating can be done in a controlled way.

### Creating a virtual environment using Intellij

Of course, one can create a python virtualenv manually in a terminal, [as explained here](https://docs.python.org/3/library/venv.html). Here we create it conveniently in Intellij.
To this end, navigate to `File > Project Structure` and then on the left to `Project Settings > Project`. In `Project SDK`, click on the dropdown menu, go to the bottom to `Add SDK` and click `Python SDK`.

Now pick the base interpreter of your choice to create the venv.

![](/images/tutorial-how-to-setup-a-python-project/create_venv.png)

After creating, there exists a new folder `venv` in the repo. Because of our configuration in `.gitignore`, Intellij automatically recognizes the `venv` folder as excluded from git, and displays it in red color.

### Running the `main.py` in the venv

To test the environment, we add some *Hello World* code to the`main.py` file:

![](/images/tutorial-how-to-setup-a-python-project/run_main.png)

Intellij offers a green *play* symbol on the left. Click the symbol and then `Run 'main'`. If everything works fine, on bottom of the Intellij IDE a windows becomes displayed and the program's output:

![](/images/tutorial-how-to-setup-a-python-project/run_main_output.png)

In the first line of the output, the command executed by Intellij to run the `main.py` is displayed. We see that our virtual env is used.

Intellij has automatically set up the configuration to run `main.py`. To see the details of the configuration, on top right of the Intellij window click on the scrolldown bar `main` next to the little green hammer:

![](/images/tutorial-how-to-setup-a-python-project/green_hammer.png)

and then click `Edit configurations`. As we see, the script path to `main.py`, the venv and the working directory are all set correctly.

![](/images/tutorial-how-to-setup-a-python-project/run_configurations.png)

### Installing modules

The python venv comes together with a `pip` installation. To install modules in the venv, navigate to the bottom menu bar of Intellij and click on `Terminal`. Now a terminal appears, in which the venv in automatically activated:

![](/images/tutorial-how-to-setup-a-python-project/terminal.png)

Now we can install python modules with pip in the venv, e.g. `numpy`, in the usual way: `pip install numpy`

**Remark:** Before using `pip install`, always carefully check that the venv is activated. Otherwise the module gets installed on the system's python distribution, which might cause trouble as explained above.
* To manually activate the venv in a terminal, use `source venv/bin/activate`.
* To manullay deactivate the venv, use `deactivate`.

### Fixing modules: `requirements.txt` and `pip freeze`

As indicated above, it is important to fix the modules installed in the venv in a precise way. This is done in a file named `requirements.txt`. Create this file in the repository's root and add it to git.

To keep track of the modules and version installed in the venv, the `pip freeze` command is quite helpful. It's output is exactly what we are looking for:

![](/images/tutorial-how-to-setup-a-python-project/pip_freeze.png)

By now we have only installed `numpy`, and this is displayed together with its version. The following command pipes the output of `pip freeze` to `requirements.txt`.

```
pip freeze > requirements.txt
```
Executing this each time after installing a new module keeps the `requirements.txt` up to date and fixes versions as explained above.

### Installing modules from an existing `requirements.txt`

If you clone a repository which already contains a `requirements.txt`, the following command installs all modules at once:

```
pip install -r requirements.txt
```

## Type and return value annotations

Python is not a type safe language. This means that the types of variables (`int`, `str`, `list`...) are not checked automatically by the interpreter. One can however simulate this to some extent from python version 3.7 on by annotating types of variables and of return values of methods. Here is an example:

```python
def add_numbers(x: float, y: float) -> float:
    return x + y
```

If the return type is not as annotated, Intellij will display a warning. Even though the warnings are not relevant for the python interpreter, one can take them as a kind of replacement for the non-existing type safety.

![](/images/tutorial-how-to-setup-a-python-project/return_type.png)

Using type annotations throughout a project reduces the number of error as and makes the code much better readable, for yourself and for others.

Here are some more examples. The following syntax can be used when defining a variable:

```python
x: int = 5
```

The `typing` module allows to describe even more complicated types:

```python
from typing import Dict, List

def some_method(x: Dict[str, List[int]]) -> List[float]:
    pass
```

If a variable might have the value `None`, the type `Optional` can indicate this:

```python
from typing import Optional

some_dict: dict = {'a': 1}
x: Optional[int] = some_dict.get('a') # returns an int
y: Optional[int] = some_dict.get('b') # return None
```

As a convention, if a method returns `None` anyway, it is also fine *not* to annotate this:

```python
def method_1() -> None: # this is fine
    print('hello')

def method_2(): # this is also fine, as a convention
    print('world')
```

## Logging

It is a good idea to introduce logging in the project right from the beginning. While it seems overhead for small projects, it becomes extremely helpful for debugging and deploying the system in production.

There are plenty of possibilities for logging in python, and a lot of [documentation](https://docs.python.org/3/howto/logging.html). Here is a configuration that does the job.

In the terminal with active venv, run `pip install python-json-logger` to install the pythonjsonlogger module. Don't forget to update the `requirements.txt` as above.

Then, in the folder `src/util`, create a file `custom_json_formatter.py` with the following content (taken from the [pythonjsonlogger's documentation](https://github.com/madzak/python-json-logger)):

```python
from datetime import datetime
from pythonjsonlogger import jsonlogger

# Source: https://github.com/madzak/python-json-logger

class CustomJsonFormatter(jsonlogger.JsonFormatter):
    def add_fields(self, log_record, record, message_dict):
        super(CustomJsonFormatter, self).add_fields(log_record, record, message_dict)
        if not log_record.get('timestamp'):
            now = datetime.now().strftime('%Y-%m-%dT%H:%M:%S.%fZ')
            log_record['timestamp'] = now
        if log_record.get('level'):
            log_record['level'] = log_record['level'].upper()
        else:
            log_record['level'] = record.levelname
```

Now introduce the logging configuration to `main.py` as follows:
```python
import logging

from arithmetics.adding_numbers import add_numbers
from util.custom_json_formatter import CustomJsonFormatter

logger = logging.getLogger(__name__)


def main():
    _initialize_logging(log_level='INFO')

    logger.info('Starting job')

    result = add_numbers(3, 4)
    print('The result is ', result)

    logger.info('Finished job')


def _initialize_logging(log_level: str) -> None:
    log_handler = logging.StreamHandler()
    formatter = CustomJsonFormatter('%(timestamp)s %(level)s %(name)s %(message)s')
    log_handler.setFormatter(formatter)
    logging.basicConfig(level=log_level, handlers=[log_handler])


if __name__ == "__main__":
    main()
```

At this point, the `main.py` already produces logging output. Of course, we want to introduce logging in other python files in our project as well. This works as in the following example method, which is called in our `main.py`:

```python
import logging

logger = logging.getLogger(__name__)


def add_numbers(x: float, y: float) -> float:
    logger.info('Start adding numbers')

    result = x + y

    logger.info('Finished adding numbers')
    return result
```

Running the `main.py` now produces the following logging output. Observe that it contains a timestamp as well as the name of the module in which the log message is created. This can be quite helpful for debugging.

```
{"timestamp": "2021-02-19T16:30:35.663634Z", "level": "INFO", "name": "__main__", "message": "Starting job"}
{"timestamp": "2021-02-19T16:30:35.663757Z", "level": "INFO", "name": "arithmetics.adding_numbers", "message": "Start adding numbers"}
{"timestamp": "2021-02-19T16:30:35.663821Z", "level": "INFO", "name": "arithmetics.adding_numbers", "message": "Finished adding numbers"}
{"timestamp": "2021-02-19T16:30:35.663887Z", "level": "INFO", "name": "__main__", "message": "Finished job"}
```

## Config files and environment variables

As for logging, in python there are plenty of possibilities to introduce a config file and read its content.

Our config is given as a yaml file. Its location is at the root of the repository in `config.yaml`.

```yaml
value_1: 'some_string'

value_2: [1, 2, 3]

value_dict:
  value_3: 'another_string'
  value_4: 10
```

### The config as a dictionary
The simplest way to read these values into the source code is just to read the yaml as a dictionary. This might be already sufficient for many projects. A good location for the method is in `src/util/config.py.` You need to install the `pyyaml` module for that.

```python
import yaml

def load_config_file(path: str) -> dict:
    with open(path, 'r') as file:
        cfg = yaml.load(file, Loader=yaml.SafeLoader)
    return cfg
```

In our `main.py`, we can use this method as follows.

```python
from pathlib import Path
import os

from util.config import load_config_file

### ...
path_to_root_directory = Path(__file__).parent.parent
config = load_config_file(path=os.path.join(path_to_root_directory, 'config.yaml'))
print(config.get('value_1'))
```
**Remark:** Note that here we use the `Path` and `os` modules to get the correct path to the config file, independent of the operating system (Linux, Mac, Windows) we are working on. On Ubuntu, we would just have `path='../config.yaml'`.


### Environment variables

To set environment variables in Intellij, navigate to the right upper menu bar and open `Edit Configurations...`:

![](/images/tutorial-how-to-setup-a-python-project/edit_configurations.png)

Under `Configuration > Environment variables` one can define the variables. As an example, we set the variable `STRING_FROM_ENV` to the value `hello`.  It is a convention to write environment variables capitalized.

![](/images/tutorial-how-to-setup-a-python-project/environment_variables.png)

An alternative, especially in case of a larger number of environment variables, is to keep the variables in a file and use [Intellij's EnvFile plugin](https://plugins.jetbrains.com/plugin/7861-envfile) to read the file (also see the button in next to `Configuration` in the screenshot above).


Now we can read the environment variables as follows:

```python
import os

env = os.environ
string_from_env = env.get('STRING_FROM_ENV', default='default_string')
```

Observe that we set default value to handle the case that the variable might not be set. Note further that `os.environ` can be treated like a dictionary and accessed by the `.get` method.


### The config as a class with type checking
Simply reading the config file as a dictionary has several disadvantages, which become more relevant in more complex situations:
* It is not checked if the config is as expected. Variables might not be set or of the wrong type. This might cause an error while the program is running - in the worst case this happens after the program already ran for a longer time. We would like to have this error raised right at the beginning, or, even better, we would like to have this tested.
* If the config is just a dict, it is unclear which keys it contains. This is a source for typing errors. It would be nice to have Intellij's suggestions at hand hand while coding.
  ![](/images/tutorial-how-to-setup-a-python-project/config_suggestions.png)
* It would also be convenient to have variables from the config file and from the environment in one config object. It might also be desirable to overwrite a config value by an environment value.

There is a package `yamldataclassconfig`  [(see here)](https://pypi.org/project/yamldataclassconfig/) which fulfills the first two of our requirements. It translates a config yaml file into a `dataclass`. It is, however, some work to bring it together with the environment variables.

Here is a solution which fulfills all three requirements. Recall that our config yaml looks as follows:

```yaml
value_1: 'some_string'

value_2: [1, 2, 3]

value_dict:
  value_3: 'another_string'
  value_4: 10
```

We read the file and translate it into a python object.

* Observe how the config structure is imitated by class variables.
* Every time we access a value, its type is checked to be as expected.
* If sub-dictionaries occur in the config file, they are translated into a sub-class inside the `Config` class. In the example, the content of `value_dict` is translated into the class `ValueDict`.
* This translation has to be done manually. However, in practice is not so much work, as the structure around can be copy & pasted and one only has to adjust the config structure itself.

```python
import os
import yaml


class Config:
    def __init__(self, path: str):
        self.path = path

        # reading values from config file
        cfg = self.load_config_file()
        self.value_1 = check(cfg.get('value_1'), str)
        self.value_2 = check(cfg.get('value_2'), list)
        self.value_dict = self.ValueDict(check(cfg.get('value_dict'), dict))

        # reading values from environment
        env = os.environ
        self.string_from_env = check(env.get('STRING_FROM_ENV'), str)

    class ValueDict:
        def __init__(self, value_dict: dict):
            self.value_3 = check(value_dict['value_3'], str)
            self.value_4: int = check(value_dict['value_4'], int)

    def load_config_file(self) -> dict:
        with open(self.path, 'r') as file:
            cfg = yaml.load(file, Loader=yaml.SafeLoader)
        return cfg


def check(x, t):
    if isinstance(x, t):
        return x
    else:
        raise Exception(f'{x} is not of type {t}')
```

In our `main.py`, the config is introduced as follows. The variables can now be accessed conveniently as class variables.

```python
from pathlib import Path
import os
from util.config import Config

# ...
path_to_root_directory = Path(__file__).parent.parent
config = Config(path=os.path.join(path_to_root_directory, 'config.yaml'))

print(config.value_2)
```

## Unit testing
Each part of the productive source code should be tested. The law is: if you don't test some part of your code, it *will* cause trouble some day.

### The folder structure
It is natural to choose the structure of the tests analogously to the structure of the source code:

![](/images/tutorial-how-to-setup-a-python-project/test_folder_structure.png)

It has the advantages that tests are easy to find (for yourself and for others), and that becomes immediately clear if some part of the code is not tested.

### Testing with pytest in Intellij

There are many different unit testing frameworks in python. The most popular one is probably `pytest`. Install it in the venv via `pip install pytest`.

We write a simple test for our example method `add_numbers`:

```python
from arithmetics.adding_numbers import add_numbers


def test_adding_numbers():
    assert add_numbers(2, 3) == 5
    assert add_numbers(1, 2) == 3
```

Now we would like to run this test with pytest in Intellij. To this end we navigate to the `Edit configurations` menu:

![](/images/tutorial-how-to-setup-a-python-project/edit_configurations.png)

add a pytest configuration:

![](/images/tutorial-how-to-setup-a-python-project/add_pytest.png)

for which we then configure the path to the test we want to run as the script path:

![](/images/tutorial-how-to-setup-a-python-project/pytest_script_path.png)

Hitting `Apply` and `OK`, a new run configuration appears in the right upper menu bar:

![](/images/tutorial-how-to-setup-a-python-project/pytest_run.png)

Clicking the play button indeed runs the test:

![](/images/tutorial-how-to-setup-a-python-project/pytest_run_successful.png)

### Enable logging in a test run

As one can see in the screenshot above, the logging messages that we introduced in `add_numbers` are not displayed by default. To active the log messages, in the `test` folder we create a file `pytest.ini` with the following content:

```
[pytest]
python_classes = !TestResult
log_cli = true
log_cli_level = INFO
log_cli_format = %(asctime)s [%(levelname)8s] %(message)s (%(filename)s:%(lineno)s)
log_cli_date_format=%Y-%m-%d %H:%M:%S
```

Running the test again, the log messages are now displayed.

```
-------------------------------- live log call ---------------------------------
2021-02-22 19:39:48 [    INFO] Start adding numbers (adding_numbers.py:7)
2021-02-22 19:39:48 [    INFO] Finished adding numbers (adding_numbers.py:11)
2021-02-22 19:39:48 [    INFO] Start adding numbers (adding_numbers.py:7)
2021-02-22 19:39:48 [    INFO] Finished adding numbers (adding_numbers.py:11)
```


















