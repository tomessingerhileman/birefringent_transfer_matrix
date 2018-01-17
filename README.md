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
"""
