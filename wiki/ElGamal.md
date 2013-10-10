---
title: ElGamal
permalink: wiki/ElGamal/
layout: wiki
---

Fix *p* a prime and *g* an integer. The powers of *g* form a subgroup
*G* inside the group *Z*<sub>*p*</sub>, which is that of integers modulo
*p*. The choice of these *p* and *g* is important so that they meet the
[Decisional
Diffie-Hellman](http://en.wikipedia.org/wiki/Decisional_Diffie%E2%80%93Hellman_assumption)
assumption; but there are standard techniques for doing that.

Say Bob generates
*P**r**i**v**K**B* = *x*, *P**u**b**K**B* = *g*<sup>*x*</sup> and makes
the latter public.

ElGamal encryption
------------------

Alice needs a random ephemeral key *w*.

  
Alice encrypts *m* ∈ *G* as
{*m*}<sub>*P**u**b**K**B*</sub> = (*g*<sup>*w*</sup>, *g*<sup>*x*</sup><sup>*w*</sup>*m*).

Bob decrypts (*u*, *v*) as *v*/*u*<sup>*x*</sup>.

Indeed,
*v*/*u*<sup>*x*</sup> = *g*<sup>*x**w*</sup>*m*/*g*<sup>*w**x*</sup> = *m*.

Schnorr signatures
------------------

  
Bob signs *m* ∈ *G* as
*S**I**G*<sub>*B*</sub>(*m*)=(*r* − *x**e*, *H*(*m*.*g*<sup>*w*</sup>)).

Alice verifies (*s*, *e*) checking that
*e* = *H*(*m*.*g*<sup>*s*</sup>*g*<sup>*x*</sup><sup>*e*</sup>).

Indeed,
*g*<sup>*w* − *x**e*</sup>*g*<sup>*x*</sup><sup>*e*</sup> = *g*<sup>*w*</sup>.


