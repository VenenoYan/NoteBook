## 其他几个程序可能用到的检测平台环境
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import pathlib
import subprocess

from dotenv import Dotenv


def get_dotenv(filename='.env'):
    return Dotenv(str(pathlib.Path(__file__).parent / filename))


def sh(*args):
    proc = subprocess.Popen(args, stdout=subprocess.PIPE)
    stdout, _ = proc.communicate()
    return stdout


def get_log_path(name):
    path = pathlib.Path(__file__).parent / 'logs' / name
    path.parent.mkdir(parents=True, exist_ok=True)
    return path
```
### auto_coffee
```python
#!/usr/bin/env python3
#-*- coding: utf-8 -*-
#coffee-auto
import datetime
import telnetlib
import time

from hackerutils import sh

COFFEE_MACHINE_ADDR = '10.10.42.42'
COFFEE_MACHINE_PASS = '1234'
COFFEE_MACHINE_PROM = 'Password: '


def main():
    # Skip on weekends.
    if datetime.date.today().weekday() in (0, 6,):
        return

    # Exit early if no sessions with my_username are found.
    if not any(s.startswith(b'my_username ') for s in sh('who').split(b'\n')):
        return

    time.sleep(17)

    conn = telnetlib.Telnet(host=COFFEE_MACHINE_ADDR)
    conn.open()
    conn.expect([COFFEE_MACHINE_PROM])
    conn.write(COFFEE_MACHINE_PASS)

    conn.write('sys brew')
    time.sleep(64)

    conn.write('sys pour')
    conn.close()


if __name__ == '__main__':
    main()
```