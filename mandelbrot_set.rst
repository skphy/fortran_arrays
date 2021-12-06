#. Computing and plotting Mandelbrot set using fortran and matplotlib
	
	.. code-block:: fortran

		program Mandelbrot
		use types, only: dp
		use constants, only: I
		use utils, only: savetxt, linspace, meshgrid
		implicit none

		integer, parameter :: ITERATIONS = 100
		integer, parameter :: DENSITY = 1000
		real(dp) :: x_min, x_max, y_min, y_max
		real(dp), dimension(DENSITY, DENSITY) :: x, y
		complex(dp), dimension(DENSITY, DENSITY) :: c, z
		integer, dimension(DENSITY, DENSITY) :: fractal
		integer :: n
		x_min = -2.68_dp
		x_max = 1.32_dp
		y_min = -1.5_dp
		y_max = 1.5_dp

		call meshgrid(linspace(x_min, x_max, DENSITY), &
		    linspace(y_min, y_max, DENSITY), x, y)
		c = x + I*y
		z = c
		fractal = 255

		do n = 1, ITERATIONS
		    print "('Iteration ', i0)", n
		    where (abs(z) <= 10) z = z**2 + c
		    where (fractal == 255 .and. abs(z) > 10) fractal = 254 * (n-1) / ITERATIONS
		end do

		print *, "Saving..."
		call savetxt("fractal.dat", log(real(fractal, dp)))
		call savetxt("coord.dat", reshape([x_min, x_max, y_min, y_max], [4, 1]))
		end program


	
	The generated fractal can be viewed by (you need matplotlib):

	.. code-block:: fortran
	

		from numpy import loadtxt
		import matplotlib.pyplot as plt

		fractal = loadtxt("fractal.dat")
		x_min, x_max, y_min, y_max = loadtxt("coord.dat")

		plt.imshow(fractal, cmap=plt.cm.hot,
			   extent=(x_min, x_max, y_min, y_max))
		plt.title('Mandelbrot Set')
		plt.xlabel('Re(z)')
		plt.ylabel('Im(z)')
		plt.savefig("mandelbrot.png")

	.. image:: mandelbrot_.png
