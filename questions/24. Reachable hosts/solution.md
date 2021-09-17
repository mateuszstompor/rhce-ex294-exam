# 24. Reachable hosts - Solution

Here you have an example script written in python

```python
#!/usr/bin/python3

import json
import argparse
import subprocess


GROUPS = {
  "proxy": {
    "hosts": [
      "managed1.example.com",
    ]    
  },
  "webservers": {
      "hosts": [
          "managed2.example.com",
          "managed3.example.com"
          ]
  },
  "database": {
      "hosts": [
          "managed3.example.com",
          "managed4.example.com"
          ]
      }
}


HOST_VARS = {
  "managed2.example.com": {
    "accessibility": "unknown"
  }
}


GROUP_VARS = {
  "database": {
    "accessibility": "private"
  },
  "proxy": {
    "accessibility": "public"
  }
}


def is_pingable(hostname):
    with open('/dev/null', 'r') as dev_null:
        p = subprocess.Popen('/usr/bin/ping -c 1 ' + hostname, 
        shell=True, stdout=dev_null, stderr=dev_null, stdin=dev_null)
    p.wait()
    return p.returncode == 0


def parse_arguments():
  parser = argparse.ArgumentParser()
  parser.add_argument('--list', help='List all groups and hosts', action='store_true')
  parser.add_argument('--host', help='Provides variables for a specific host')
  arguments = parser.parse_args()
  if not arguments.list and arguments.host is None:
      parser.error("You must either list all hosts or retrieve variables for a specific one")
  return arguments


def list_all():
  common = {
    "all": {
        "children": ["ungrouped"] + list(GROUPS.keys())
            
    }
  }
  reachable_hosts = {group: {'hosts': [h for h in details['hosts'] if is_pingable(h)]} for group, details in GROUPS.items()}
  return dict(**common, **reachable_hosts)


def provide_vars(host):
    groups_of_host = {name for name in GROUPS.keys() if host in GROUPS.get(name, {}).get("hosts", [])}
    base = dict()
    for name in groups_of_host:
        base = dict(**base, **GROUP_VARS.get(name, {}))
    return dict(**base, **HOST_VARS.get(host, {}))


if __name__ == '__main__':
  args = parse_arguments()
  if args.list:
      print(json.dumps(list_all()))
  else:
      if is_pingable(args.host):
        print(json.dumps(provide_vars(args.host)))
      else:
        print(json.dumps({}))
```