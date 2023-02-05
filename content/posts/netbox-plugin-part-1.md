+++ 
date = "2023-02-04T00:00:00Z" 
draft = true 
title = "Netbox Plugin Part 1" 
slug = "netbox-plugin-part-1" 
tags = ['netbox', 'ipam', 'dcim', 'python']
+++

Netbox Plugin Part 1

This is just trying to make a place to make a plugin. 

Installed Netbox as following the official instructions https://docs.netbox.dev/en/stable/installation/.

Installed cookiecutter and followed the instructions for cookiecutter Netbox Plugin [here](https://github.com/netbox-community/cookiecutter-netbox-plugin). 

The offical Netbox Plugin steps reference `virtualvenv` but i'm used to pipenv so here we go with some fresh errors. 

Using Ubuntu the apt packaged pipenv ran into some errors. Quick searched suggested to install via pip, ok. 

``` 
❯ pipenv
Traceback (most recent call last):
  File "/usr/bin/pipenv", line 33, in <module>
    sys.exit(load_entry_point('pipenv==11.9.0', 'console_scripts', 'pipenv')())
  File "/usr/lib/python3/dist-packages/pipenv/vendor/click/core.py", line 722, in __call__
    return self.main(*args, **kwargs)
  File "/usr/lib/python3/dist-packages/pipenv/vendor/click/core.py", line 696, in main
    with self.make_context(prog_name, args, **extra) as ctx:
  File "/usr/lib/python3/dist-packages/pipenv/vendor/click/core.py", line 621, in make_context
    self.parse_args(ctx, args)
  File "/usr/lib/python3/dist-packages/pipenv/vendor/click/core.py", line 1018, in parse_args
    rest = Command.parse_args(self, ctx, args)
  File "/usr/lib/python3/dist-packages/pipenv/vendor/click/core.py", line 875, in parse_args
    parser = self.make_parser(ctx)
  File "/usr/lib/python3/dist-packages/pipenv/vendor/click/core.py", line 821, in make_parser
    for param in self.get_params(ctx):
  File "/usr/lib/python3/dist-packages/pipenv/vendor/click/core.py", line 774, in get_params
    help_option = self.get_help_option(ctx)
  File "/usr/lib/python3/dist-packages/pipenv/cli.py", line 26, in get_help_option
    from .import core
  File "/usr/lib/python3/dist-packages/pipenv/core.py", line 21, in <module>
    import requests
  File "/usr/lib/python3/dist-packages/pipenv/vendor/requests/__init__.py", line 65, in <module>
    from . import utils
  File "/usr/lib/python3/dist-packages/pipenv/vendor/requests/utils.py", line 27, in <module>
    from .cookies import RequestsCookieJar, cookiejar_from_dict
  File "/usr/lib/python3/dist-packages/pipenv/vendor/requests/cookies.py", line 172, in <module>
    class RequestsCookieJar(cookielib.CookieJar, collections.MutableMapping):
AttributeError: module 'collections' has no attribute 'MutableMapping'
```

So remove that, slap on some pipenv via pip and then get another error which required the removal of setuptools. 
Pretty sure i'm going to need that later on so downgrading my be the only way forward based on [this](https://github.com/pypa/pipenv/issues/5075) and [this](https://github.com/pypa/setuptools/issues/3278). 

```
❯ python3 -m pipenv shell
Creating a virtualenv for this project...
Pipfile: /home/pete/src/netbox_vzsubcalc_plugin/Pipfile
Using /usr/bin/python3 (3.10.6) to create virtualenv...
⠸ Creating virtual environment...created virtual environment CPython3.10.6.final.0-64 in 136ms
  creator CPython3Posix(dest=/home/pete/.local/share/virtualenvs/netbox_vzsubcalc_plugin-78q0gtL0, clear=False, no_vcs_ignore=False, global=False)
  seeder FromAppData(download=False, pip=bundle, setuptools=bundle, wheel=bundle, via=copy, app_data_dir=/home/pete/.local/share/virtualenv)
    added seed packages: pip==22.0.2, setuptools==59.6.0, wheel==0.37.1
  activators BashActivator,CShellActivator,FishActivator,NushellActivator,PowerShellActivator,PythonActivator

✔ Successfully created virtual environment!
Traceback (most recent call last):
  File "/usr/lib/python3.10/runpy.py", line 196, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.10/runpy.py", line 86, in _run_code
    exec(code, run_globals)
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/__main__.py", line 4, in <module>
    cli()
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/vendor/click/core.py", line 1128, in __call__
    return self.main(*args, **kwargs)
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/cli/options.py", line 57, in main
    return super().main(*args, **kwargs, windows_expand_args=False)
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/vendor/click/core.py", line 1053, in main
    rv = self.invoke(ctx)
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/vendor/click/core.py", line 1659, in invoke
    return _process_result(sub_ctx.command.invoke(sub_ctx))
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/vendor/click/core.py", line 1395, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/vendor/click/core.py", line 754, in invoke
    return __callback(*args, **kwargs)
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/vendor/click/decorators.py", line 84, in new_func
    return ctx.invoke(f, obj, *args, **kwargs)
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/vendor/click/core.py", line 754, in invoke
    return __callback(*args, **kwargs)
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/cli/command.py", line 402, in shell
    do_shell(
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/core.py", line 2641, in do_shell
    ensure_project(
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/core.py", line 541, in ensure_project
    ensure_virtualenv(
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/core.py", line 474, in ensure_virtualenv
    do_create_virtualenv(
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/core.py", line 1060, in do_create_virtualenv
    project._environment = Environment(
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/environment.py", line 79, in __init__
    self._base_paths = self.get_paths()
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/environment.py", line 383, in get_paths
    c = subprocess_run(command)
  File "/home/pete/.local/lib/python3.10/site-packages/pipenv/utils/processes.py", line 75, in subprocess_run
    return subprocess.run(
  File "/usr/lib/python3.10/subprocess.py", line 501, in run
    with Popen(*popenargs, **kwargs) as process:
  File "/usr/lib/python3.10/subprocess.py", line 969, in __init__
    self._execute_child(args, executable, preexec_fn, close_fds,
  File "/usr/lib/python3.10/subprocess.py", line 1845, in _execute_child
    raise child_exception_type(errno_num, err_msg, err_filename)
FileNotFoundError: [Errno 2] No such file or directory: '/home/pete/.local/share/virtualenvs/netbox_vzsubcalc_plugin-78q0gtL0/bin/python'
```

So the offical netbox plugin instructions say to do this needful. 

```
python3 -m venv ~/.virtualenvs/my_plugin
echo /opt/netbox/netbox > $VENV/lib/python3.8/site-packages/netbox.pth
```

But I'm using the pipenv so  we'll go with

```
❯ python3 -m pipenv shell
Launching subshell in virtual environment...
 . /home/pete/.local/share/virtualenvs/netbox_vzsubcalc_plugin-78q0gtL0/bin/activate
```

And then the echo command can be. 

```
echo /opt/netbox/netbox > ~/.local/share/virtualenvs/netbox_vzsubcalc_plugin-78q0gtL0/lib/python3.10/site-packages/netbox.pth
```


```
❯ python setup.py develop
running develop
/home/pete/.local/share/virtualenvs/netbox_vzsubcalc_plugin-78q0gtL0/lib/python3.10/site-packages/setuptools/command/easy_install.py:158: EasyInstallDeprecationWarning: easy_install command is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
/home/pete/.local/share/virtualenvs/netbox_vzsubcalc_plugin-78q0gtL0/lib/python3.10/site-packages/setuptools/command/install.py:34: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
running egg_info
creating netbox_vzsubcalc_plugin.egg-info
writing netbox_vzsubcalc_plugin.egg-info/PKG-INFO
writing dependency_links to netbox_vzsubcalc_plugin.egg-info/dependency_links.txt
writing top-level names to netbox_vzsubcalc_plugin.egg-info/top_level.txt
writing manifest file 'netbox_vzsubcalc_plugin.egg-info/SOURCES.txt'
reading manifest file 'netbox_vzsubcalc_plugin.egg-info/SOURCES.txt'
reading manifest template 'MANIFEST.in'
warning: no previously-included files matching '__pycache__' found under directory '*'
warning: no previously-included files matching '*.py[co]' found under directory '*'
warning: no files found matching '*.rst' under directory 'docs'
warning: no files found matching 'conf.py' under directory 'docs'
warning: no files found matching 'Makefile' under directory 'docs'
warning: no files found matching 'make.bat' under directory 'docs'
warning: no files found matching '*.jpg' under directory 'docs'
warning: no files found matching '*.png' under directory 'docs'
warning: no files found matching '*.gif' under directory 'docs'
adding license file 'LICENSE'
writing manifest file 'netbox_vzsubcalc_plugin.egg-info/SOURCES.txt'
running build_ext
Creating /home/pete/.local/share/virtualenvs/netbox_vzsubcalc_plugin-78q0gtL0/lib/python3.10/site-packages/netbox-vzsubcalc-plugin.egg-link (link to .)
Adding netbox-vzsubcalc-plugin 0.1.0 to easy-install.pth file

Installed /home/pete/src/netbox_vzsubcalc_plugin
Processing dependencies for netbox-vzsubcalc-plugin==0.1.0
Finished processing dependencies for netbox-vzsubcalc-plugin==0.1.0
```

So need to start Netbox back up again. 

```
cd /opt/netbox/netbox/
source /opt/netbox/venv/bin/activate
