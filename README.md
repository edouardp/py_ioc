py_ioc
======

Pythonic IOC Container for Dependancy Injection.

Dependancy Injection is designed to seperate the standard configuration of an object hierarchy from
it's construction. 

Usage
=====

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
a = c.Adder()
a.add(1,2)
# Outputs:
#   Logging 'Adding 2 and 3' to screen
# Returns:
# 3
