#. Example showing the data storage in Fortran and excessing it (VERY IMPORTANT)
	- I input an array of shape(2,3) as input and see how fortran stores it and print it?
	- Answer: data is stored column wise and can be printed rowwise or columnwise depending upon the print, write statement. By 
		default, data is print in column major order. Kindly see the output of the following program.
		

	.. code-block:: fortran

		program test
			!
			! .. author: SKumar
			! .. date: Dec2018
			! .. updated: 2021
			!
			USE numtypes, ONLY : dp

			implicit none

			INTEGER :: i, j

			!REAL(dp) :: x(2,2)
			REAL(dp) :: x(2,3)

			!x = reshape([1._dp, 4._dp, 9._dp, 10._dp], [2, 2])
			x = reshape([1._dp, 4._dp,         &
						 9._dp, 10._dp,        &
						-1._dp, -2._dp      ], &
						[2, 3])

			print *, 'rows of x:', size(x,1)
			print * , 'columns of x:', size(x,2)

			DO j = 1, size(x,1) ! row
				WRITE(*,*) 'row', j
				WRITE(*,*) (x(j,i), i=1,size(x,2))
			ENDDO
			!write(*,*) REPEAT('*+*=*', 10)
			!WRITE(*,*) x

			WRITE(*,*) REPEAT('*',50)
			WRITE(*,*) 'column elements:'

			WRITE(*,*) 'column 1'
			WRITE(*,*) x(:,1)

			WRITE(*,*) 'column 2'
			WRITE(*,*) x(:,2)

			WRITE(*,*) 'column 3'
			WRITE(*,*) x(:,3)
			WRITE(*,*) REPEAT('*',50)
		end program test
		
	Output: 
		(compiled and linked using: ifort -o test.x test.f90 -I/home/sonu/f_util -L/home/sonu/f_util -lf_util)
		(./test.x)
	
	.. code-block: fortran

		 rows of x:           2
		 columns of x:           3
		 row           1
		   1.00000000000000        9.00000000000000       -1.00000000000000     
		 row           2
		   4.00000000000000        10.0000000000000       -2.00000000000000     
		 **************************************************
		 column elements:
		 column 1
		   1.00000000000000        4.00000000000000     
		 column 2
		   9.00000000000000        10.0000000000000     
		 column 3
		  -1.00000000000000       -2.00000000000000     
		 **************************************************	
		
		
