Tags: #software-engineering #python #scientific-computing 

Below is a class that provides basic quantization floating point values via rounding to a fixed number of significant digits.  The intent is to allow said quantized values to be used without having to care that floating point values are approximations.

```python
class QuantizedFloat( object ):
    """
    Class that quantizes a floating point value to a specific level of precision.  Explicit
    comparisons use the quantized floating point value while strict ordering comparisons
    use the wrapped value directly.  QuantizedFloats are hashable so they may be used
    containers that require this property (e.g. sets), with the hashed value being
    derived from the quantized value.

    It is intended that this wrapper allows containers to ignore the vagaries of
    floating point representations by using the user-specified precision to
    partition floating point numbers into equivalent classes.
    """

    def __init__( self, value, precision=13 ):
        """
        Constructs a FloatWithEpsilonBall object.

        Takes 2 arguments:

          value     - The floating point value of interest.
          precision - Number of significant digits to round value to when comparing
                      it against other floating point values for equality.  If
                      omitted, defaults to 13 digits.

        Returns 1 value:

          self - The constructed object.

        """

        # we quantize the provided value by rounding it to precision-many
        # significant digits.
        scale_factor = 10.0**precision

        # keep track of the original value and the quantized version, along with
        # the precision used to get from the former to the latter.
        self._value           = value
        self._precision       = precision
        self._quantized_value = math.floor( value * scale_factor ) / scale_factor

    def __lt__( self, other ):
        """
        Less than predicate.  The original value is compared against the other's
        __float__() representation.

        Takes 1 argument:

          other - Floating point-like object to compare against.  Must have a
                  __float__() method.

        Returns 1 value:

          less_than_flag - True if self's value is strictly less than the other
                           value.

        """

        return self.__float__() < other.__float__()

    def __eq__( self, other ):
        """
        Fuzzy equality predicate.  The quantized value is compared against the
        other's __float__() representation with a 10^(-precision) epsilon ball
        around it.

        Takes 1 argument:

          other - Floating point-like object to compare against.  Must have a
                  __float__() method.

        Returns 1 value:

          equality_flag - True if the other's __float__() representation is
                          within a 10^(-precision) epsilon ball of self's
                          quantized value.

        """

        return math.isclose( self._quantized_value, other, abs_tol=10**(-self._precision) )

    def __float__( self ):
        """
        Returns a floating point representation of the wrapped value.

          NOTE: This uses the wrapped value rather than the quantized value so
                that "normal" uses are oblivious to the wrapper class.

        Takes no arguments.

        Returns 1 value:

          float_value - The floating point representation of the wrapped value.

        """

        # attempt to generate a floating point representation out of the value
        # we've wrapped, otherwise use the wrapped value directly.
        if hasattr( self._value, "__float__" ):
            return self._value.__float__()
        else:
            return self._value

    def __hash__( self ):
        """
        Returns a hashed representation of the wrapped value.  The quantized version of
        the wrapped value is used so that distinct values that are close to each other
        are considered the same.

        Takes no arguments.

        Returns 1 value:

           hashed_value - Hashed representation of the quantized version of the
                          wrapped value.

        """

        return hash( "{:f}".format( self.quantize() ) )

    def __repr__( self ):
        """
        Returns a deserializable representation of the object.

        Takes no arguments.

        Returns 1 value:

          repr_string - String representation of the object.

        """

        return "QuantizedFloat( {}, {:d} )".format( self._value, self._precision )

    def quantize( self ):
        """
        XXX

        Takes no arguments.

        Returns 1 value:

          quantized_value -

        """

        return self._quantized_value

```