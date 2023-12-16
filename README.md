# manim-import-test
Running MacOS Sonoma ARM, installation of manim detailed [here](https://github.com/3b1b/manim/issues/2050#issuecomment-1858666104); I am using `pipenv` with `pyenv`, python version 3.8.18.
For some reason, all my import statements fail. Project directory is located on my computer (myComputer) at /Users/myUser/manim-import-test.

# setup

In the directory execute:

`pipenv install`

which outputs:

```
Creating a virtualenv for this project...
Pipfile: /Users/myUser/manim-import-test/Pipfile
Using /Users/myUser/.pyenv/versions/3.8.18/bin/python3.8 (3.8.18) to create virtualenv...
⠙ Creating virtual environment...created virtual environment CPython3.8.18.final.0-64 in 127ms
  creator CPython3Posix(dest=/Users/myUser/.local/share/virtualenvs/manim-import-test-Az11BCfe, clear=False, no_vcs_ignore=False, global=False)
  seeder FromAppData(download=False, pip=bundle, setuptools=bundle, wheel=bundle, via=copy, app_data_dir=/Users/myUser/Library/Application Support/virtualenv)
    added seed packages: pip==23.3.1, setuptools==69.0.2, wheel==0.42.0
  activators BashActivator,CShellActivator,FishActivator,NushellActivator,PowerShellActivator,PythonActivator

✔ Successfully created virtual environment!
Virtualenv location: /Users/myUser/.local/share/virtualenvs/manim-import-test-Az11BCfe
Installing dependencies from Pipfile.lock (fe3792)...
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

Now establish the `pipenv` enviornment with:

`pipenv shell`

which outputs:

```
Launching subshell in virtual environment...
 . /Users/myUser/.local/share/virtualenvs/manim-import-test-Az11BCfe/bin/activate
myUser@myComputer manim-import-test %  . /Users/myUser/.local/share/virtualenvs/manim-import-test-Az11BCfe/bin/activate
```

## error

When executing the test:
`manimgl test.py`

the output is as follows:

```
ManimGL v1.6.1
[19:15:37] INFO     Using the default configuration file, which    
                    you can modify in                                           
                    `/Users/myUser/.local/share/virtualenvs/manim-im              
                    port-test-Az11BCfe/lib/python3.8/site-packages              
                    /manimlib/default_config.yml`                               
           INFO     If you want to create a local configuration    
                    file, you can create a file named                           
                    `custom_config.yml`, or run `manimgl --config`              
Traceback (most recent call last):
  File "/Users/myUser/.local/share/virtualenvs/manim-import-test-Az11BCfe/bin/manimgl", line 8, in <module>
    sys.exit(main())
  File "/Users/myUser/.local/share/virtualenvs/manim-import-test-Az11BCfe/lib/python3.8/site-packages/manimlib/__main__.py", line 21, in main
    config = manimlib.config.get_configuration(args)
  File "/Users/myUser/.local/share/virtualenvs/manim-import-test-Az11BCfe/lib/python3.8/site-packages/manimlib/config.py", line 300, in get_configuration
    module = get_module(args.file)
  File "/Users/myUser/.local/share/virtualenvs/manim-import-test-Az11BCfe/lib/python3.8/site-packages/manimlib/config.py", line 184, in get_module
    spec.loader.exec_module(module)
  File "<frozen importlib._bootstrap_external>", line 843, in exec_module
  File "<frozen importlib._bootstrap>", line 219, in _call_with_frames_removed
  File "test.py", line 1, in <module>
    from imp_ext import *
ModuleNotFoundError: No module named 'imp_ext'
```

Observe `test.py` and `imp_ext.py` are in the same directory, where the former consists solely of a single import statement - `test.py` importing `imp_ext.py`, `imp_ext.py` being an empty file.
