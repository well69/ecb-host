stolen from https://github.com/lrntplc/ecb-host
for working code go to his very well designed and well thought out board.
the point of forking is to extract as much useful code as possible for use in my own chessboard which is powered by a raspberry pi rather than an edison


# Foldable, Intel Edison powered, chess board project

This is the host side part, that will run on Intel Edison.

## File list:
 * EcbDriver.py - the drivers for Top/Bottom Half and Command Controllers;
 * EcbFSM.py    - the finite state machine
 * ecb.py       - the main file
 * start_ecb.sh - wrapper script to launch the software from systemd;
 * ecb.service  - systemd service file;

## Installation on Edison (assuming you do it in the home directory):
### * Create the Python environment first:

<pre><code>$ pip install virtualenv
$ virtualenv --system-site-packages ecb
$ source ecb/bin/activate
$ pip install python-chess
$ pip install futures
$ pip install python-socketio
$ pip install Flask
$ deactivate</code></pre>

### * Create a new directory inside the ecb environment directory:

`$ mkdir ecb/ecb`

### * Copy the files from your host machine to Edison:

`$ scp -r EcbDriver.py EcbFSM.py ecb.py start_ecb.sh ecb.service static/ root@edison.local:ecb/ecb/`

### * Install the systemd service:

<pre><code>$ cp ecb/ecb/ecb.service /lib/systemd/system/
$ systemctl enable ecb
$ systemctl start ecb</code></pre>
