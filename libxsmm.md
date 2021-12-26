Tags: #scientific-computing 

# Calling from Fortran
Can call functions directly from Fortran 2003, and newer, via the `ISO_C_BINDING` interface.  

## Examples
libxsmm [Github example](https://github.com/hfp/libxsmm/blob/master/samples/utilities/dispatch/dispatch_udt.f).  

Listing 1.1 from ["Efficiency of High Order SEM on Petascale Architecture"](https://www.alcf.anl.gov/files/isc16_nek.pdf):
```fortran
logical, save :: init = .false.  
type(LIBXSMM_DMM_FUNCTION), save :: xmm1, xmm2, xmm3  

! lazy initialization of function-private function pointers  
! to eliminate dispatching overhead  
if (.not. init) then  
    call libxsmm_dispatch(xmm1, nx, ny*nz, nx, 1.0_dp, 0.0_dp)  
    call libxsmm_dispatch(xmm2, nx, ny, ny, 1.0_dp, 0.0_dp)  
    call libxsmm_dispatch(xmm3, nx*ny, nz, nz, 1.0_dp, 0.0_dp)  
    init = .true.  
endif  

! element-local operation  
call libxsmm_call(xmm1, C_LOC(wddx), C_LOC(u(1,1,1)), C_LOC(work1))  
do iz=1,nz  
    call libxsmm_call(xmm2, C_LOC(u(1,1,iz)), C_LOC(wddyt), C_LOC(work2(1,1,iz)))  
enddo  
call libxsmm_call(xmm3, C_LOC(u(1,1,1)), C_LOC(wddzt), C_LOC(work3))  

! element update  
au(:,:,:) = h1* ( work1*gx + work2*gy + work3*gz ) + h2*b*u
```

# Benchmarking
Provides a simple tool to benchmark matrix multiplications.  See [[Benchmarking libxsmm Performance]].