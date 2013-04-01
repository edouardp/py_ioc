py_ioc
======

Pythonic IOC Container for Dependancy Injection.

Dependancy Injection is designed to seperate the standard configuration of an object hierarchy from
it's construction. 

Usage
=====

```python
from IOC import ioc, Container

@ioc
class Config():
  def __init__(self, logfile='log.txt'):
    self.logfile = logfile

@ioc
class FileLogger:
    def __init__(self, config=None):
        self.config = config
    def log(self, s):
        print "Logging '{0}' to file '{1}'".format(s, self.config.logfile)

@ioc
class Adder:
    def __init__(self, logger=None):
        self.logger = logger
    def add(self,a,b):
        self.logger.log("Adding {0} and {1}".format(a,b))
        return a+b 

c = Container()
c.add_class_factories(logger=FileLogger, config=Config)
c.add_instance(logfile='fnord.txt')
a = c.Adder()
a.add(1,2)
# Outputs:
#   Logging 'Adding 1 and 2' to file 'fnord.txt'
# Returns:
# 3
```

Goals
-----

To by __pythonic__, meaning that the implementation is as simple and direct as
is reasonable, and that there is as little "magic" as possible. It also
means that only those parts of IOC/DI that make sense in Python are implemented,
and none of the parts that are nessessary purely because of being implmented
in static languages like Java or C#.

To be __useful__, in that it can be used to solve real world problems.

To be __small__, so that it is easy to understand, maintain and extend.

To be __retrofittable__, so it can be applied to existing classes without
needing them to be modified first.


TODO
----

- Handle classes without __init__() methods
- Handle different objects lifetimes (singleton and weak singleton)
- Handle error paths
