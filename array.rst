#. To initialize an array, do:

    integer :: r(5)
    
    r = [1, 2, 3, 4, 5]

    This syntax is valid since the Fortran 2003 standard and it is the preferred syntax (the old syntax r = (/ 1, 2, 3, 4, 5 /) 
    should only be used if you cannot use Fortran 2003).
    
#. Integer division

    If N is an integer: (N - 1.0_dp)/N    will give your real. 
    
    If 1 is used in place of 1.0_dp then integer output, which may be not the required output you want!!
    
#. Private in module

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
    For details see the link: https://www.fortran90.org/src/best-practices.html
