#. To initialize an array, do:

    integer :: r(5)
    
    r = [1, 2, 3, 4, 5]

    This syntax is valid since the Fortran 2003 standard and it is the preferred syntax (the old syntax r = (/ 1, 2, 3, 4, 5 /) 
    should only be used if you cannot use Fortran 2003).
    
#. Integer division

    If N is an integer: (N - 1.0_dp)/N    will give your real. 
    
    If 1 is used in place of 1.0_dp then integer output, which may be not the required output you want!!
    
#. Private in module

    .. code-block:: fortran

        module test
            use types, only: dp, sp
            use utils, only: stop_err
            implicit none

            private
            ...
            ..
        end module test    
    
    the `private` is empty here => all your subroutines/data types will be private to the module by default.

#. assumed shape array vs explicit shape array
    use assumed shape array in subroutines. But, if you want to interface your fortran program with c, python, and so on, better use explicit 
    shape array. 
    For details see the link: https://www.fortran90.org/src/best-practices.html. This is `fortran90 website <https://www.fortran90.org>`_ 
    a beautiful explanation give here for fortran and its comparison with the python afaik. 
    
    - example of using assumed shape array:
    
        When passing arrays in and out of a subroutine/function, use the following pattern for 1D arrays (it is called assumed-shape):
        
        .. code-block:: fortran

            subroutine f(r)
                real(dp), intent(out) :: r(:)
                integer :: n, i
                n = size(r)
                do i = 1, n
                    r(i) = 1.0_dp / i**2
                enddo
            end subroutine

        2D arrays:
        
        .. code-block:: fortran
        
            subroutine g(A)
                real(dp), intent(in) :: A(:, :)
                ...
            end subroutine

        and call it like this:

        .. code-block:: fortran

            real(dp) :: r(5)
            call f(r)


