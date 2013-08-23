---
title: Sigma Protocols
permalink: wiki/Sigma_Protocols/
layout: wiki
---

In general
----------

Sigma protocols involve a verifier (A) and prover (B). They suppose that
Alice and Bob share a public input *v* and agree on an efficiently
testable relation *R*, and that Bob pretends to have a private input
*w*:

-   such that (*v*, *w*)∈*R*;
-   which he does does not want to disclose.

Through the protocol, Bob will seek to convince Alice.

The protocol has three rounds:

*B* → *A* : *a* = *a*(*v*, *R*, *w*)

*A* → *B* : *c* = *c*(*v*, *R*, *a*)

*B* → *B* : *r* = *r*(*v*, *R*, *w*, *a*, *c*, *w*)
 Lastly, Alice checks that Bob response *r* to her challenge *r* is
valid. This explains what the last two rounds are for. The first round
is there out of technical necessity: Bob chooses this *a* as a mask for
passing the challenge without disclosing *w*.

Example
-------

Here is an example based on Discrete Logarithms. Take *p* a prime and
*g* an integer. The powers of *g* form a subgroup *G*<sub>*q*</sub>
(having *q* elements) inside the group *Z*<sub>*p*</sub> (having *p*
elements), which is that of integers modulo *p*. The choice of these *p*
and *g* is important so that they meet the [Decisional
Diffie-Hellman](http://en.wikipedia.org/wiki/Decisional_Diffie%E2%80%93Hellman_assumption)
assumption; but there are standard techniques for doing that.

-   Public input *v* ∈ *G*<sub>*q*</sub>.
-   Agreed relation (*v*, *w*)∈*R* ⇔ *g*<sup>*w*</sup> = *v*.
-   Private input *w*.
-   Bob will need some random *u* ∈ *Z*<sub>*p*</sub>, Alice will need
    some random *c* ∈ *Z*<sub>*p*</sub>.

The protocol has three rounds:

*B* → *A* : *a* = *g*<sup>*u*</sup>

*A* → *B* : *c*

*B* → *B* : *r* = *w**c* + *u*
 Alice validates Bob response by checking that
*g*<sup>*r*</sup> = *a**h*<sup>*c*</sup>. Indeed,

*g*<sup>*r*</sup> = *g*<sup>*w**c*</sup>*g*<sup>*u*</sup> = *h*<sup>*c*</sup>*a*.

