##LMOMENT PYTHON LIBRARY:

This file contains the lmoments.f library created by:
      J. R. M. HOSKING                                                   
      IBM RESEARCH DIVISION                                              
      T. J. WATSON RESEARCH CENTER                                       
      YORKTOWN HEIGHTS                                                   
      NEW YORK 10598, U.S.A.      
      AUGUST    1996

The base Fortran code is copyright of the IBM Corperation, and the licensing
information is shown below:

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
IBM software disclaimer

LMOMENTS: Fortran routines for use with the method of L-moments
Permission to use, copy, modify and distribute this software for any purpose
and without fee is hereby granted, provided that this copyright and permission
notice appear on all copies of the software. The name of the IBM Corporation
may not be used in any advertising or publicity pertaining to the use of the
software. IBM makes no warranty or representations about the suitability of the
software for any purpose. It is provided "AS IS" without any express or implied
warranty, including the implied warranties of merchantability, fitness for a
particular purpose and non-infringement. IBM shall not be liable for any direct,
indirect, special or consequential damages resulting from the loss of use,
data or projects, whether in an action of contract or tort, arising out of or
in connection with the use or performance of this software.
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

All methodologies in this library are repeated from this source file verbatim,
with the exception of the samlmu() function.  This was redesigned to take
advantage of pythons language, as direct FORTRAN conversion of the method
did not translate speed.

This library was designed to use L-moments to predict optimal parameters
for a number of distributions.  Distributions supported in this file are
listed below, with their distribution suffix:
    *Exponential (EXP)
    *Gamma (GAM)
    *Generalised Extreme Value (GEV)
    *Generalised Logistic (GLO)
    *Generalised Normal (GNO)
    *Generalised Pareto (GPA)
    *Gumbel (GUM)
    *Kappa (KAP)
    *Normal (NOR)
    *Pearson III (PE3)
    *Wakeby (WAK)
    *Weibull (WEI)

The primary function in this file is the samlmu(x,nmom) function, which takes
an input dataset x and  input of the number of moments to produce the log
moments of that dataset.

For Instance, given a list "Data", if 5 l-moments are needed, the function
would be called by lmom.samlmu(Data,5)

In this file contains four different functions for using each distribution.
Each function can be called by the prefix FUN with the suffix DIS.

*PEL: (x,nmom):
      Parameter Estimates.  This takes the L-Moments calculated by samlmu()
      and predicts the parameter estimates for that function.
      
      EXAMPLE: Find Wakeby distribution that best fits dataset DATA:

      import lmom
      para = lmom.pelwak(lmom.samlmu(DATA,5))

*QUA: (f,para)
      Quartile Estimates.  This takes the parameter estimates for a
      distribution, and a given quartile value to calculate the quartile for the
      given function.

      EXAMPLE: Find the Upper Quartile (75%) of the Kappa distribution that
      best fits dataset DATA:

      import lmom
      para = lmom.pelkap(lmom.samlmu(DATA,5))
      UQ = lmom.quakap(0.75,para)

*LMR: (para,nmom):
      L-Moment Ratios.  This takes the parameter estimates for a distribution
      and calculates nmom L-Moment ratios.

      EXAMPLE: Find 4 lmoment ratios for the Gumbel distribution that
      best fits dataset DATA:

      import lmom
      para = lmom.pelgum(lmom.samlmu(DATA,5))
      LMR = lmom.lmrgum(para,4)

*CDF: (x,para):
      Cumulative Distribution Function.  This takes the parameter estimates
      for a distribution and calculates the quartile for a given value x.

      EXAMPLE: Find the quartile of the datapoint 6.4 for the Weibull
      Distribution that best fits the dataset DATA:

      import lmom
      para = lmom.pelwei(lmom.samlmu(DATA,5))
      quartile = lmom.quawei(6.4,para)

Python Translation conducted by:
    Sam Gillespie
    Numerical Analyst
    C&R Consulting
    Townsville Australia
    June 2013

For more information, or to report bugs, contact:
    sam@candrconsulting.com.au

Licensing for Python Translation:
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Copyright (c) 2013 C&R Consulting.
All rights reserved.

Redistribution and use in source and binary forms are permitted
provided that the above copyright notice and this paragraph are
duplicated in all such forms and that any documentation,
advertising materials, and other materials related to such
distribution and use acknowledge that the software was developed
by the C&R Consulting.  The name of the
C&R Consulting may not be used to endorse or promote products derived
from this software without specific prior written permission.
THIS SOFTWARE IS PROVIDED ``AS IS'' AND WITHOUT ANY EXPRESS OR
IMPLIED WARRANTIES, INCLUDING, WITHOUT LIMITATION, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
"""
