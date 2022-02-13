# Project 01: Integrals and geometry read-in
This project will introduce you to the basics of Fortran input/output, and manipulation of arrays. The aim is to read files containing the Gaussian integrals, precomputed from [Psi4](https://psicode.org/psi4manual/master/index.html), and a file specifying the geometry of the system.
## Step 1: Reading integral files
These files are present in each integral/geometry file directory
| File name | Explanation |
|--|--|
| `s.dat` | The AO overlap integrals, $S_{\mu\nu}=\langle \psi_{\mu}\vert\psi_{\nu}\rangle$ |
|`t.dat`|The AO kinetic integrals, $T_{\mu\nu}=\langle \psi_{\mu}\vert -\frac{1}{2}\nabla^2\vert\psi_{\nu}\rangle$|
|`v.dat`|The AO potential integrals, $V_{\mu\nu}=\langle \psi_{\mu}\vert V_\mathrm{ext}\vert\psi_{\nu}\rangle$|
|`eri.dat`|The AO electron repulsion integrals, $(\mu\nu\vert\sigma\tau)=\langle\mu\tau\vert\sigma\nu\rangle=\int\int\psi^*_{\mu}(1)\psi_{\nu}(1)\frac{1}{r_{12}}\psi^*_{\sigma}(2)\psi_{\tau}(2)dr_1dr_2$|
|`geom.dat`|The complete specification of the molecule in a Cartesian matrix|
#### One-electron integrals
The one electron files are specified as follows
	
	1 1  1.000000000000000
	2 1  0.236703936510848
	2 2  1.000000000000000
	3 1 -0.000000000000000
	3 2  0.000000000000000
Where the first two integers are the bra and ket basis function indices respectively. Create a derived type that holds the one-electron integral arrays, and read them in.
````{admonition} Hint 1: Creating the derived type 
:class: tip, dropdown
Derived types in Fortran are like structs in C and classes (without class-bound functions) in Python. The layout of a derived type declaration is as follows
```{code-block} fortran
module integrals
   implicit none
   ! Conventionally derived type names are suffixed with `_t`
   type int_store_t
      real, dimension(:,:), allocatable :: ovlp, ke, ele_nuc
   end type int_store_t
end module integrals
```
````
````{admonition} Hint 2: What size arrays should we allocate? 
:class: tip, dropdown
At this point, we don't know the number of basis functions, so we can't allocate the integral arrays just yet! We can get the number of basis functions most easily from `s.dat` by just getting the largest index. To do that you need to open up the file and read through it once first without storing anything into the `ovlp` array.
```{code-block} fortran
subroutine read_integrals_in(int_store)
   ! This is an intrinsic I/O parameter (constant), which we can compare our I/O status variable to, to see if we've reached the end of the file.
   use, intrinsic :: iso_fortran_env, only: iostat_end
   
   ! Remember we just defiined the derived type above, which should be in the same `integrals` module, so we don't have to say `use int_store_t`.
   type(int_store_t), intent(inout) :: int_store

   integer :: ir, ios, nbasis, ibasis, jbasis
   real :: intgrl

   nbasis = 0
   ! 'newunit=ir' gurantees the file is opened in a new file stream, 'old' means we're reading an existing file, and 'formatted' means plain text.
   open(newunit=ir, file='dat/s.dat', status='old', form='formmated')
   ! Pass through the file once to find nbasis first
   do
      ! We read from the 'ir' file stream, which has our file open, '*' means default formatting options, 'iostat' is the I/O status which we need to keep track to know when we reach the end.
      ! We read two integers and a real from each line, into the variables.
      read(ir, *, iostat=ios) ibasis, jbasis, intgrl 
      ! Break loop if EOF reached
      if (ios==iostat_end) exit
      if (ibasis>nbasis .or. jbasis>nbasis) then
         nbasis = max(ibasis, jbasis)
      end if
   end do

   ! Close the file
   close(ir)
```
````
````{admonition} Hint 3: Reading in one-electron integrals
:class: tip, dropdown