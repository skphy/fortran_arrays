#. assign an array to a variable 'a' having 10 elements of float type
  
  .. code-block:: fortran
  	  
	  Real(dp) :: a(10)
	  ! this defines a 1D array of length 10 with float values
	  ! dp means double precision i.e. kind type of array;  used to defined the precision and range of the array `a`
	  !
	  a = [1.,2.,3.,4.,5.,5.,6,7,8,9,10.1]
	  
#. kind types in fortran for real arrays
	
	
	- for real data/array there are 3 kind types:
		kind=4, kind=8, and  kind=16 ... (for details see the link `web gcc.gnu.org<https://gcc.gnu.org/onlinedocs/gfortran/KIND-Type-Parameters.html>`_ as 
		well as `intel website<https://www.intel.com/content/www/us/en/develop/documentation/fortran-compiler-oneapi-dev-guide-and-reference/top/language-reference/a-to-z-reference/q-to-r/real-function.html>_).
		
	
