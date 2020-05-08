---
layout: post
title: Creating executable for 3 different OS
category: web
tags: [python, pyinstaller, pyenv, electron, mac]
---

The app needs to read/write from serial. Build in macOS Catalina. Error due to version sucks.

### Electron

- Was able to read serial using nodejs serialport
- Versioning error when trying to read the serial from electron
- Fix the version to the older ones [from here](https://github.com/serialport/electron-serialport):
    ```json
    "electron": "5.0.11",
    "electron-rebuild": "1.8.6"
    "serialport": "^7.1.5"
	```
- [How to](https://girishjoshi.io/post/access-serialport-from-electron-application-and-creating-gui-for-micropython-repl-on-esp8266/) read and write to serial from the html

### PyInstaller

- `pyserial` is supported by PyInstaller
- Tried with the python3 default from Catalina, does not work `OSError: Python library not found: libpython3.7.dylib, libpython3.7m.dylib, Python, .Python`
- While searching, found that people uses `pyenv` to get the library, so
    ```bash
	# Install pyenv
	brew update
	brew install pyenv

	# Set up pyenv in bash
	git clone https://github.com/pyenv/pyenv.git ~/.pyenv
	echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
	echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
	echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile

	# Install python
	env PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install 3.7.3
	which python        # will return ~/.pyenv/shims/python not the default python anymore
	pyenv versions      # will list out different python installed in the system
	pyenv global 3.7.3  # uses python version 3.7.3

	# Install packages
	pip -V              # check if it comes from pyenv
	pip install pyinstaller pyserial
	```
- Make the executable by `python -m PyInstaller test.py`, running pyinstaller directly didn't work. This will create a folder with a bunch of libraries inside.
- To generate one executable, `python -m PyInstaller -c --clean --onefile test.py`
