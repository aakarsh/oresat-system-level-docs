# OreSat System Level Documentation

[![License](https://img.shields.io/github/license/oresat/oresat-system-level-docs)](./LICENSE)
[![Issues](https://img.shields.io/github/issues/oresat/oresat-system-level-docs)](https://github.com/oresat/oresat-system-level-docs/issues)
[![Documentation Status](https://readthedocs.org/projects/oresat-system-level-docs/badge/?version=latest)](https://oresat-system-level-docs.readthedocs.io/en/latest/?badge=latest)

## Manually building the docs

- Install dependencies:
  - On Arch Linux: `$ sudo pacman -S python-sphinx python-sphinx-rtd-theme`
  - On Debian Linux: `$ sudo apt install python3-sphinx python3-sphinx-rtd-theme`
  - With pip: `$ pip install sphinx sphinx-rtd-theme`
- Build docs: `$ make html`
- Open `build/html/index.html` in a browser.
