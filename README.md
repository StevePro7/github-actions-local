# github-actions-local
Testing GitHub Actions on local host using act utiltiy

python.exe -m venv .venv
.\.venv\Scripts\activate
OR
source .venv/bin/activate


touch .github/workflows/hello-world.yml

Mac
act push
error::The version '3.11' with architecture 'x64' was not found for this operating system.%0AThe list of all available versions can be found here: https://raw.githubusercontent.com/actions/python-versions/main/versions-manifest.json

ChatGPT
Thanks for the context — you're using act to run GitHub Actions locally on your Mac, which explains the issue.

act uses Docker to simulate GitHub Actions runners. However, it doesn't come with all the preinstalled Python versions like GitHub-hosted runners do.

Option 1: Use a Custom Docker Image with Python 3.11 Preinstalled

Run act with an image that has Python 3.11 installed:
act push --container-architecture linux/amd64 -P ubuntu-latest=ghcr.io/catthehacker/ubuntu:act-latest

This worked!
Here are the logs


act push --container-architecture linux/amd64 -P ubuntu-latest=ghcr.io/catthehacker/ubuntu:act-latest
INFO[0000] Using docker host 'unix:///var/run/docker.sock', and daemon socket 'unix:///var/run/docker.sock' 
[Hello World Python/hello-world] ⭐ Run Set up job
[Hello World Python/hello-world] 🚀  Start image=ghcr.io/catthehacker/ubuntu:act-latest
[Hello World Python/hello-world]   🐳  docker pull image=ghcr.io/catthehacker/ubuntu:act-latest platform=linux/amd64 username= forcePull=true
[Hello World Python/hello-world]   🐳  docker create image=ghcr.io/catthehacker/ubuntu:act-latest platform=linux/amd64 entrypoint=["tail" "-f" "/dev/null"] cmd=[] network="host"
[Hello World Python/hello-world]   🐳  docker run image=ghcr.io/catthehacker/ubuntu:act-latest platform=linux/amd64 entrypoint=["tail" "-f" "/dev/null"] cmd=[] network="host"
[Hello World Python/hello-world]   🐳  docker exec cmd=[node --no-warnings -e console.log(process.execPath)] user= workdir=
[Hello World Python/hello-world]   ✅  Success - Set up job
[Hello World Python/hello-world]   ☁  git clone 'https://github.com/actions/setup-python' # ref=v5
[Hello World Python/hello-world] ⭐ Run Main Checkout code
[Hello World Python/hello-world]   🐳  docker cp src=/Users/stevepro/GitHub/StevePro7/github-actions-local/. dst=/Users/stevepro/GitHub/StevePro7/github-actions-local
[Hello World Python/hello-world]   ✅  Success - Main Checkout code [324.392881ms]
[Hello World Python/hello-world] ⭐ Run Main Set up Python
[Hello World Python/hello-world]   🐳  docker cp src=/Users/stevepro/.cache/act/actions-setup-python@v5/ dst=/var/run/act/actions/actions-setup-python@v5/
[Hello World Python/hello-world]   🐳  docker exec cmd=[/opt/acttoolcache/node/18.20.8/x64/bin/node /var/run/act/actions/actions-setup-python@v5/dist/setup/index.js] user= workdir=
[Hello World Python/hello-world]   ❓  ::group::Installed versions
| Version 3.11 was not found in the local cache
| Version 3.11 is available for downloading
| Download from "https://github.com/actions/python-versions/releases/download/3.11.13-15433298024/python-3.11.13-linux-22.04-x64.tar.gz"
| Extract downloaded archive
| [command]/usr/bin/tar xz --warning=no-unknown-keyword --overwrite -C /tmp/9fc5eaa7-5972-4056-a244-f1fd3c0c75f2 -f /tmp/0b09a27c-a619-40d3-a528-d5cb7ca882de
| Execute installation script
| Check if Python hostedtoolcache folder exist...
| Creating Python hostedtoolcache folder...
| Create Python 3.11.13 folder
| Copy Python binaries to hostedtoolcache folder
| Create additional symlinks (Required for the UsePythonVersion Azure Pipelines task and the setup-python GitHub Action)
| Upgrading pip...
| Looking in links: /tmp/tmpm1ej3cv5
| Requirement already satisfied: setuptools in /opt/hostedtoolcache/Python/3.11.13/x64/lib/python3.11/site-packages (65.5.0)
| Requirement already satisfied: pip in /opt/hostedtoolcache/Python/3.11.13/x64/lib/python3.11/site-packages (24.0)
[Hello World Python/hello-world]   ❗  ::error::WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
| Collecting pip
| Downloading pip-25.1.1-py3-none-any.whl.metadata (3.6 kB)
| Downloading pip-25.1.1-py3-none-any.whl (1.8 MB)
| ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.8/1.8 MB 1.7 MB/s eta 0:00:00
| 
| Installing collected packages: pip
| Attempting uninstall: pip
| Found existing installation: pip 24.0
| Uninstalling pip-24.0:
| Successfully uninstalled pip-24.0
| Successfully installed pip-25.1.1
| Create complete file
| Successfully set up CPython (3.11.13)
[Hello World Python/hello-world]   ❓  ::endgroup::
[Hello World Python/hello-world]   ❓ add-matcher /run/act/actions/actions-setup-python@v5/.github/python.json
[Hello World Python/hello-world]   ✅  Success - Main Set up Python [34.563984881s]
[Hello World Python/hello-world]   ⚙  ::set-env:: pythonLocation=/opt/hostedtoolcache/Python/3.11.13/x64
[Hello World Python/hello-world]   ⚙  ::set-env:: PKG_CONFIG_PATH=/opt/hostedtoolcache/Python/3.11.13/x64/lib/pkgconfig
[Hello World Python/hello-world]   ⚙  ::set-env:: Python_ROOT_DIR=/opt/hostedtoolcache/Python/3.11.13/x64
[Hello World Python/hello-world]   ⚙  ::set-env:: Python2_ROOT_DIR=/opt/hostedtoolcache/Python/3.11.13/x64
[Hello World Python/hello-world]   ⚙  ::set-env:: Python3_ROOT_DIR=/opt/hostedtoolcache/Python/3.11.13/x64
[Hello World Python/hello-world]   ⚙  ::set-env:: LD_LIBRARY_PATH=/opt/hostedtoolcache/Python/3.11.13/x64/lib
[Hello World Python/hello-world]   ⚙  ::set-output:: python-version=3.11.13
[Hello World Python/hello-world]   ⚙  ::set-output:: python-path=/opt/hostedtoolcache/Python/3.11.13/x64/bin/python
[Hello World Python/hello-world]   ⚙  ::add-path:: /opt/hostedtoolcache/Python/3.11.13/x64
[Hello World Python/hello-world]   ⚙  ::add-path:: /opt/hostedtoolcache/Python/3.11.13/x64/bin
[Hello World Python/hello-world] ⭐ Run Post Set up Python
[Hello World Python/hello-world]   🐳  docker exec cmd=[/opt/acttoolcache/node/18.20.8/x64/bin/node /var/run/act/actions/actions-setup-python@v5/dist/cache-save/index.js] user= workdir=
[Hello World Python/hello-world]   ✅  Success - Post Set up Python [367.824256ms]
[Hello World Python/hello-world] ⭐ Run Complete job
[Hello World Python/hello-world] Cleaning up container for job hello-world
[Hello World Python/hello-world]   ✅  Success - Complete job
[Hello World Python/hello-world] 🏁  Job succeeded