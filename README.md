# Requirements
- Python 3
- pip
- virtualenv
- ansible
- git
- virtualbox
- vagrant

# Installation
1. Type in terminal:
```bash
VENVDIR=oleh-venv
python3 -m venv $VENVDIR # run if venv is missing: apt install python3.12-venv
source $VENVDIR/bin/activate
pip install -U -r requirements.txt
```
2. Run Vagrant:
```bash
vagrant up
```