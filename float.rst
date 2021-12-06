Floating Point Numbers
----------------------

#. Somewhere create and export a parameter dp:

    integer, parameter:: dp=kind(0.d0)                   ! double precision

    and declare floats as:

    real(dp) :: a, b, c

    Always write all floating point constants with the _dp suffix:

    1.0_dp, 3.5_dp, 1.34e8_dp

    and never any other way 
