# Install & Upgrade

#### Install phidata <a href="#install-phidata" id="install-phidata"></a>

We recommend installing `phidata` using `pip` in a python virtual environment

1

Create a virtual environment

Open the `Terminal` and create a python virtual environment.

MacWindows

Copy

```
python3 -m venv ~/.venvs/aienv
source ~/.venvs/aienv/bin/activate
```

2

Install phidata

Install the latest version of `phidata`

MacWindows

Copy

```
pip install -U phidata
```

If you encounter errors, try updating pip using `python -m pip install --upgrade pip`

***

#### [​](https://docs.phidata.com/how-to/install#upgrade-phidata)Upgrade phidata <a href="#upgrade-phidata" id="upgrade-phidata"></a>

To upgrade `phidata`, run this inside your virtual environment

Copy

```
pip install -U phidata --no-cache-dir
```
