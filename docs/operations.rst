Formatting
==========

Naming
------

In addition to containing a mean and standard deviation, :py:class:`.Measurement`
objects can also have a string name and unit associated with it.
These can then be used both in printing values and in labelling any plots
created with these values.  By default, :py:class:`.Measurement` objects are named
unnamed_var0, with a unique number assigned to each object.
The name and units of a :py:class:`.Measurement` object can be declared either when the
object is created or altered after.

.. nbinput:: ipython3

   import qexpy as q
	
   x = q.Measurement(10, 1, name='Length', units='cm')
   # This value can be changed using the following method
	
   x.rename(name='Cable Length', units='m')
   # Note that units are only a marker and changing units does not change
   # any values with a Measurement
	
   print(x)
	
.. nboutput:: ipython3

   Cable Length = 10 +/- 1

Units
-----

Values which have more complicated units can also be entered using the
following syntax.  Consider a measurement of acceleration, with units of
m/s^2 or meters per second squared. This can be entered as a string of the
unit letters raised to the their respective powers:
	
.. nbinput:: ipython3

   import qexpy as q
	
   t = q.Measurement(3, 0.25, name='Time', units='s')
   a = q.Measurement(10, 1, name='Acceleration', units='m^1 s^-2')

This also allows for the units of values produced by operations such as
multiplication to be generated automatically.  Consider the calculation of
the velocity of some object that accelerates at a for t seconds:

.. nbinput:: ipython3

   v = a*t
   print(v.units)
	
.. nboutput:: ipython3

	{'m': 1, 's': -1}
	
This unit list, when used in a plot will appear as:

.. code-block:: python

   'm^1 s^-1'

Print Styles
------------

The default format of printing a value with an uncertainty is:
   
.. nbinput:: ipython3
   
   import qexpy as q
   x = q.Measurement(10, 1)
   print(x)

.. nboutput:: ipython3

   10 +/- 1
	
However, there are two other ways of outputting a :py:class:`.Measurement` object.
Furthermore, each method also allows for a specific number of significant
digits to be shown.

One method is called scientific and will output the number in scientific
notation with the error being shown as a value with only a single whole 
digit.  In order to change between any printing method, the following
function will change how the package prints a :py:class:`.Measurement` object:

.. nbinput:: ipython3

   import qexpy as q
	
   x = q.Measurement(122, 10)
   q.set_print_style("Scientific")
   print(x)
	
.. nboutput:: ipython3

   (12 +/- 1)*10**1
	
The same process is used for a print style called Latex which, as the name
suggests, is formatted for use in Latex documents.  This may be useful in
the creation of labs by allowing variables to be copied and pasted
directly into a Latex document.

.. nbinput:: ipython3

   import qexpy as q
	
   x = q.Measurement(122, 10)
   q.set_print_style("Latex")
   print(x)
	
.. nboutput:: ipython3

   (12 \pm 1)\e1

Significant Figures
-------------------

By default, QExPy will use the least significant figure in the uncertainty as the least significant figure. This won’t affect any of the calculations, but becomes apparent when printing the value of a :py:class:`Measurement`. The number of significant figures displayed when a :py:class:`Measurement` is printed can be changed using a the following function.

.. automethod:: qexpy.error.set_sigfigs
   :noindex:
   
.. nbinput:: ipython3
   
   import qexpy as q
   x = q.Measurement(10, 1)
   y = x/3
   q.set_sigfigs(3)
   print(y)

.. nboutput:: ipython3

   3.333 +/- 0.333
