```
<project_name>/
├── README.md
├── .venv/
│   ├── bin/
│   │   ├── activate
│   │   ├── activate.csh
│   │   ├── activate.fish
│   │   ├── Activate.psX
│   │   ├── pip*
│   │   ├── pipX*
│   │   ├── pip3.XX*
│   │   ├── python -> python3.XX*
│   │   ├── pythonX -> python3.XX*
│   │   └── python3.XX -> /usr/local/bin/pythonX.XX*
│   ├── .gitignore
│   ├── include/
│   │   └── python3.XX/
│   ├── lib/
│   │   └── python3.XX/
│   ├── lib64 -> lib/
│   └── pyvenv.cfg
└── <project_name>.py
```

### To Create Virtual Environments:
To use system python:
```
python -m venv .venv
```
This will create a folder named `.venv` containing all the required stuff. Adding `.venv` to the
project `.gitignore` will appropriately hide all the gross guts.

To specify a particular python:
```
python3.XX -m venv .venv
```
For example, calling `python3.12` will create a virtual envirnment that uses python3.12.
####
To activate, from within the project folder:
```
source .venv/bin/activate
```
#### To Deactivate:
```
deactivate
```
### Pip!:
To install packages, use the following after the virtual environemnt is activated:
```
pip install <pkg>
```
After packages are install, the following can create a file that be used to recreate the current environment:
```
pip freeze >> requirements.txt
```
To recreate the environment:
```
pip install -r requirements.txt
```
### Install new version of python
###### Here's how python3.13 was installed:
First a new version of python was downloaded from the official python download page and extracted.
```
wget https://www.python.org/ftp/python/3.13.2/Python-3.13.2.tar.xz
mv Python-3.13.2.tar.xz ~/Downloads/
cd ~/Downloads/
tar -xJf Python-3.13.2.tar.xz
cd Python-3.13.2/
```
Then system packages were updated in preparation.
```
sudo apt update
sudo apt upgrade
```
The following is only required in order to get all the fun goodies, like SQLite intergration and ncurses:
```
sudo apt-get install build-essential gdb lcov pkg-config \
     libbz2-dev libffi-dev libgdbm-dev libgdbm-compat-dev liblzma-dev \
     libncurses5-dev libreadline6-dev libsqlite3-dev libssl-dev \
     lzma lzma-dev tk-dev uuid-dev zlib1g-dev libmpdec-dev
```
Otherwise, only the bare minimum build dependencies are installed:
```
sudo apt-get build-dep python3
sudo apt-get install pkg-config
```
Only one or the other are required!
Finally we configure and make, and end with installing:
```
./configure --enable-optimizations
make
sudo make install
```
