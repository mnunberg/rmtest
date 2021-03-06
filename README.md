# rmtest

A simple nano-framework for testing redis modules using python unit test, and a disposable ephemeral redis subprocess.

## Example:

```py

import unittest
from rmtest import ModuleTestCase

class MyTestCase(ModuleTestCase('../module.so', module_args = ('foo', 'bar'))):
            
    def testCmd(self):
        with self.redis() as r:
          
            self.assertOk(r.execute_command('mymodule.dosomething', 'foo', 'bar'))

if __name__ == '__main__':
    unittest.main()               
    
```

## Controlling parameters with Environment Variables

It is possible to control the path to the redis server executable, the path to the module and an optional fixed port, from environment variables.

### REDIS_MODULE_PATH

Controls the path to the module, either absolute, or relative to where the test resides.

### REDIS_PATH

Controls the path to redis-server. By default we assume it's in `$PATH`

### REDIS_PORT

Causes the tests to run against a fixed redis port instead of spawning ephemeral disposable redis instances for each test. 

This is useful for debugging failures with `redis-cli MONITOR`.


## Installing from pypi

```sh
$ pip install rmtest
```

## Installing from Git

1. Clone this repo

2. `sudo python setup.py install`
