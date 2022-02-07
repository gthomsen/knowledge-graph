Tags: #software-engineering #python 

Collection of things I didn't know about Python and probably should.

# Properties
Used to annotate class methods as getters, setters and deleters.

From the [Python 3 documentation](https://docs.python.org/3/library/functions.html#property):

Can be specified for read-only attributes and provide a getter method when used as a decorator:
```python
class Parrot:
    def __init__( self ):
        self._voltage = 100000

    @property
    def voltage( self ):
        """Get the current voltage."""
        return self._voltage

parrot = Parrot

print( "current voltag is {:d}".format( parrow.voltage ) )
```

Or more verbosely when providing all three accessors:
```python
class C:
    def __init__( self ):
        self._x = None

    def getx( self ):
        return self._x

    def setx( self, value ):
        self._x = value

    def delx( self ):
        del self._x

    x = property( getx, setx, delx, "I'm the 'x' property." )

c = C

c.x = 3
print( "x = {:d}".format( c.x ) )
```