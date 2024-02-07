# birefringent_transfer_matrix

This program contains a set of scripts for analyzing stratified media
that vary only in the z-direction, and is infinite in the x-y plane,
with a uniaxial crystal as one or more layers. 

This implements the calculations detailed in:

T. Essinger-Hileman, "Transfer matrix for treating stratified media
including birefringent crystals," Applied Optics, 512:2, 212-218 (2013)

It can also translate the transfer matrix of a stack to Jones
and Mueller matrices, and can calculate polarized transmission, reflection,
and absorption properties of the stack.

Limitations:
** This code will only deal with the case where the
extraordinary axis is tangent to the surfaces of the crystal, at an
angle chi with the x-axis.

** The program would need to be reconsidered for biaxial crystals.

Tom Essinger-Hileman

Johns Hopkins University

March 2014


Usage:

A Stack object first needs to be created that describes the physical
system being modeled, with layers defined by their thicknesses, material
types, and relative angles (important only for birefringent materials).

Materials are defined as material objects that give indices of refraction,
loss tangents, and an identifying name.

Once a Stack object has been created, it is straightforward to calculate
the transfer matrix, along with Jones and Mueller matrices. 

Code snippet to create an AR-coated sapphire half-wave plate to illustrate:

```
  import numpy as np
  import transfer_matrix as tm

  GHz = 1e9 
  deg = 180/np.pi

  sapphire = tm.material( 3.07, 3.41, 2.3e-4, 1.25e-4, 'Sapphire', materialType='uniaxial')
  duroid   = tm.material( 1.715, 1.715, 1.2e-3, 1.2e-3, 'RT Duroid', materialType='isotropic')

  thicknesses = [305e-6, 3.15*tm.mm, 305e-6]
  materials   = [duroid, sapphire, duroid]
  angles      = [0.0, 0.0, 0.0]
  hwp         = tm.Stack( thicknesses, materials, angles )

  TransferMatrix = tm.stackTransferMatrix( hwp, 145*GHz, 10.0*deg, 0*deg, 1.0, 1.0 )
  Mueller        = tm.Mueller( hwp, 145*GHz, 10*deg, 0*deg, reflected=False)
  Jones          = tm.Jones( hwp, 145*GHz, 10.0*deg, 0*deg, reflected=False)
  ```
  
 The reflected keyword for the Jones and Mueller matrices allows one to specify whether
 you want the matrices for transmission vs. reflection. 
 
