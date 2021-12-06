#. assign an array to a variable 'a' having 10 elements of float type
  
  .. code-block:: fortran
  	  
	  Real(dp) :: a(10)
	  ! this defines a 1D array of length 10 with float values
	  ! dp means double precision i.e. kind type of array;  used to defined the precision and range of the array `a`
	  !
	  a = [1.,2.,3.,4.,5.,5.,6,7,8,9,10.1]
	  
#. kind types in fortran for real arrays
	
	
	- for real data/array there are 3 kind types:
		kind=4, kind=8, and  kind=16 for real data (for details see the link `web gcc.gnu.org <https://gcc.gnu.org/onlinedocs/gfortran/KIND-Type-Parameters.html>`_ as well as `intel website <https://www.intel.com/content/www/us/en/develop/documentation/fortran-compiler-oneapi-dev-guide-and-reference/top/language-reference/a-to-z-reference/q-to-r/real-function.html>`_).
		
	
#. Multidimensional Arrays data handling (MOST important in Fortran90/95/2003/2018 -- better compare it with python/c/c++ arrays)
	
	Always access slices as V(:, 1), V(:, 2), or V(:, :, 1), e.g. the colons should be on the left. 
	That way the stride is contiguous and it will be fast. So when you need some slice in your algorithm, always setup 
	the array in a way, so that you call it as above. If you put the colon on the right, it will be slow.
	
	- Example:
	
	.. code-block:: fortran
		

		dydx = matmul(C(:, :, i), y) ! fast
		dydx = matmul(C(i, :, :), y) ! slow

	In other words, the “fortran storage order” is: smallest/fastest changing/innermost-loop index first, 
	largest/slowest/outermost-loop index last (“Inner-most are left-most.”). So the elements of a 3D array 
	A(N1,N2,N3) are stored, and thus most efficiently accessed, as:
		
	.. code-block:: fortran
	
		do i3 = 1, N3
		    do i2 = 1, N2
			do i1 = 1, N1
			    A(i1, i2, i3)
			end do
		    end do
		end do

	Associated array of vectors would then be most efficiently accessed as:
	
	.. code-block:: fortran
	
		do i3 = 1, N3
		    do i2 = 1, N2
			A(:, i2, i3)
		    end do
		end do

	And associated set of matrices would be most efficiently accessed as:

	.. code-block:: fortran
	
		do i3 = 1, N3
		    A(:, :, i3)
		end do

	Storing/accessing as above then accesses always contiguous blocks of memory, directly adjacent to one another; no skips/strides.

	When not sure, always rewrite (in your head) the algorithm to use strides, for example the first loop would become:

	.. code-block:: fortran
	
		do i3 = 1, N3
		    Ai3 = A(:, :, i3) !! i am getting the matrix for each value of i3  --> total of N3 matrices
		    do i2 = 1, N2
			Ai2i3 = Ai3(:, i2)  !! i am getting array for each value of i2  --> total of N2 arrays
			do i1 = 1, N1
			    Ai2i3(i1)  !!  i am getting a single data value for each value of i1  --> total of N1 values of Ai2i3
			    !
			    !! more digging of the data array: 
			    ! A(1:N1, 1:N2, 1:N3) => we have N1xN2 matrix for each value of i3 => we have N1XN2 * N3 elements in the array A.
			    !
			    ! N1XN2 matrix data is column major order
			end do
		    end do
		end do


	the second loop would become:

	.. code-block:: fortran
	
		do i3 = 1, N3
		    Ai3 = A(:, :, i3)
		    do i2 = 1, N2
			Ai3(:, i2)
		    end do
		end do


	And then make sure that all the strides are always on the left. Then it will be fast.
