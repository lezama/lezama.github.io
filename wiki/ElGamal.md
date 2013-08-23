---
title: ElGamal
permalink: wiki/ElGamal/
layout: wiki
---

Take *p* a prime and *g* an integer. The powers of *g* form a subgroup
*G*<sub>*q*</sub> (having *q* elements) inside the group
*Z*<sub>*p*</sub> (having *p* elements), which is that of integers
modulo *p*. The choice of these *p* and *g* is important so that they
meet the [Decisional
Diffie-Hellman](http://en.wikipedia.org/wiki/Decisional_Diffie%E2%80%93Hellman_assumption)
assumption; but there are standard techniques for doing that.

Say Bob generates
*P**r**i**v**K**B* = *x*, *P**u**b**K**B* = *g*<sup>*x*</sup> and makes
the latter public.

ElGamal encryption
------------------

  
Alice encrypts *m* ∈ *G*<sub>*q*</sub> as
{*m*}<sub>*P**u**b**K**B*</sub> = (*y*<sup>*r*</sup>*m*, *g*<sup>*r*</sup>).

Bob decrypts (*a*, *b*) as *a*/*b*<sup>*x*</sup>.

Indeed,
*a*/*b*<sup>*x*</sup> = *y*<sup>*r*</sup>*m*/*g*<sup>*r**x*</sup> = *g*<sup>*x**r*</sup>*m*/*g*<sup>*r**x*</sup> = *m*.

Schnorr signatures
------------------

  
Bob signs *m* ∈ *G*<sub>*q*</sub> as
*S**I**G*<sub>*B*</sub>(*m*)=(*r* − *x**e*, *H*(*m*.*g*<sup>*r*</sup>)).

Alice verifies (*s*, *e*) checking that
*e* = *H*(*m*.*g*<sup>*s*</sup>*y*<sup>*e*</sup>).

Indeed,
*g*<sup>*s*</sup>*y*<sup>*e*</sup> = *g*<sup>*r* − *x**e*</sup>*g*<sup>*x**e*</sup> = *g*<sup>*r*</sup>.


