# BLOCX. Sentinel


> An automated governance helper for BLOCX
Sentinel is an autonomous agent for persisting, processing and automating BLOCX governance objects and tasks. It is a Python application which runs alongside the BLOCX instance on each BLOCX Masternode.

## Table of Contents

- [Install](#install)
  - [Dependencies](#dependencies)
- [Usage](#usage)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)

## Install

These instructions cover installing Sentinel on Ubuntu 18.04 / 20.04.

### Dependencies

Update system package list and install dependencies:

    $ sudo apt-get update
    $ sudo apt-get -y install git python3 virtualenv

Make sure Python version 3.6.x or above is installed:

    python3 --version

Make sure the local BlocX daemon running is at least version 0.15.0.

    $ blocxd --version | head -n1

### Install Sentinel

Clone the Sentinel repo and install Python dependencies.

    $ git clone https://github.com/BLOCXTECH/sentinel.git && cd sentinel
    $ virtualenv -p $(which python3) ./venv
    $ ./venv/bin/pip install -r requirements.txt

## Usage

Sentinel is "used" as a script called from cron every minute.

### Set up Cron

Set up a crontab entry to call Sentinel every minute:

    $ crontab -e

In the crontab editor, add the lines below, replacing '/path/to/sentinel' to the path where you cloned sentinel to:

    * * * * * cd /path/to/sentinel && ./venv/bin/python bin/sentinel.py >/dev/null 2>&1

## Configuration

Configuration is done via environment variables. Example:

```sh
$ RPCUSER=blocx RPCPASSWORD=password RPCHOST=127.0.0.1 RPCPORT=12971 ./venv/bin/python bin/sentinel.py
```

A path to a `blocx.conf` file can be specified in `sentinel.conf`:

    # warning: deprecated
    blocx_conf=/path/to/blocx.conf

This is now deprecated and will be removed in a future version. Users are encouraged to update their configurations to use environment variables instead.

## Troubleshooting

To view debug output, set the `SENTINEL_DEBUG` environment variable to anything non-zero, then run the script manually:

    $ SENTINEL_DEBUG=1 ./venv/bin/python bin/sentinel.py
