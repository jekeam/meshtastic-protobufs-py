# Meshtastic Protobuf Definitions

[![CI](https://img.shields.io/github/actions/workflow/status/meshtastic/protobufs/ci.yml?branch=master&label=actions&logo=github&color=yellow)](https://github.com/meshtastic/protobufs/actions/workflows/ci.yml)
[![CLA assistant](https://cla-assistant.io/readme/badge/meshtastic/protobufs)](https://cla-assistant.io/meshtastic/protobufs)
[![Fiscal Contributors](https://opencollective.com/meshtastic/tiers/badge.svg?label=Fiscal%20Contributors&color=deeppink)](https://opencollective.com/meshtastic/)
[![Vercel](https://img.shields.io/static/v1?label=Powered%20by&message=Vercel&style=flat&logo=vercel&color=000000)](https://vercel.com?utm_source=meshtastic&utm_campaign=oss)

## Overview

The [Protobuf](https://developers.google.com/protocol-buffers) message definitions for the Meshtastic project (used by apps and the device firmware).

**[Documentation/API Reference](https://buf.build/meshtastic/protobufs)**

# For Python use python_gen 
## Example:
```python
import importlib
import os
import sys


# IMPORTANT: Indicate the exact path to the folder where the folder `meshtastic` with *_pb2.py lies
# Example for your structure:
PB2_PARENT = r"C:\my_github\LoRa\protobufs\python_gen"

# ------------- Подготовка импорта локальных pb2 -------------
if not os.path.isdir(PB2_PARENT):
    raise SystemExit(f"PB2_PARENT was not found: {PB2_PARENT}. Generate PB2 and put the Meshtastic folder there.")

# вставляем в начало sys.path — чтобы локальные pb2 перекрывали site-packages
if PB2_PARENT not in sys.path:
    sys.path.insert(0, PB2_PARENT)

print(f"[i] PB2 parent: {PB2_PARENT} (inserted into sys.path)")

# List of candidate modules for finding the desired types (local)
CANDIDATE_MODULES = [
    "meshtastic.meshtastic_pb2",
    "meshtastic.protobuf.meshtastic_pb2",
    "meshtastic.admin_pb2",
    "meshtastic.protobuf.admin_pb2",
    "meshtastic.protobuf.channel_pb2",
    "meshtastic.channel_pb2",
    "meshtastic.portnums_pb2",
    "meshtastic.protobuf.portnums_pb2",
    "meshtastic.mqtt_pb2",
    "meshtastic.protobuf.mqtt_pb2",
    "meshtastic_pb2",
    "admin_pb2",
    "channel_pb2",
    "portnums_pb2",
]

_imported = {}


def try_import(name):
    if name in _imported:
        return _imported[name]
    try:
        m = importlib.import_module(name)
        _imported[name] = m
        print(f"[i] imported {name}")
        return m
    except Exception:
        _imported[name] = None
        return None


# I import all the candidates (faster than searching for attributes later)
for nm in CANDIDATE_MODULES:
    try_import(nm)
```

## Stats

![Alt](https://repobeats.axiom.co/api/embed/47e9ee1d81d9c0fdd2b4b5b4c673adb1756f6db5.svg "Repobeats analytics image")
