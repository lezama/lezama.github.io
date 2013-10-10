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

*B* → *A* : *r* = *r*(*v*, *R*, *w*, *a*, *c*, *w*)
 Lastly, Alice checks that Bob response *r* to her challenge *r* is
valid. This explains what the last two rounds are for. The first round
is there out of technical necessity: Bob chooses this *a* as a mask for
passing the challenge without disclosing *w*.

Building blocks
---------------

Here are examples of Sigma protocols based on the hardness of Discrete
Logarithms. Fix *p* a prime and *g* an integer. The powers of *g* form a
subgroup *G* inside the group *Z*<sub>*p*</sub>, which is that of
integers modulo *p*. The choice of these *p* and *g* is important so
that they meet the [Decisional
Diffie-Hellman](http://en.wikipedia.org/wiki/Decisional_Diffie%E2%80%93Hellman_assumption)
assumption; but there are standard techniques for doing that.

**Ex. 1: Schnorr identification protocol**

-   Public input *v* ∈ *G*.
-   Agreed relation (*v*, *w*)∈*R* ⇔ *g*<sup>*w*</sup> = *v*.
-   Private input *w*.
-   Bob will need some random *s* ∈ *Z*<sub>*p*</sub>.
-   Alice will need some random *c* ∈ *Z*<sub>*p*</sub>.

The protocol has three rounds:

*B* → *A* : *a* = *g*<sup>*s*</sup>

*A* → *B* : *c*

*B* → *A* : *r* = *w**c* + *s*
 Alice validates Bob response by checking that
*g*<sup>*r*</sup> = *v*<sup>*c*</sup>*a*. Indeed, if Bob was honest it
should be that

*g*<sup>*r*</sup> = *g*<sup>*w*</sup><sup>*c*</sup>*g*<sup>*s*</sup> = *v*<sup>*c*</sup>*a*

**Ex. 2: Diffie-Hellman pairs**

Fix another *h* an integer. The powers of *h* form a subgroup *H* inside
the group *Z*<sub>*p*</sub>.

-   Public input *u* ∈ *G*, *v* ∈ *H*.
-   Agreed relation
    ((*u*, *v*),*w*)∈*R* ⇔ *g*<sup>*w*</sup> = *u* ∧ *h*<sup>*w*</sup> = *v*.
-   Private input *w*.
-   Bob will need some random *s* ∈ *Z*<sub>*p*</sub>.
-   Alice will need some random *c* ∈ *Z*<sub>*p*</sub>.

The protocol has three rounds:

*B* → *A* : *a* = *g*<sup>*s*</sup>

*A* → *B* : *c*

*B* → *A* : *r* = *w**c* + *s*
 Alice validates Bob response by checking that
*g*<sup>*r*</sup> = *u*<sup>*c*</sup>*a* and that
*h*<sup>*r*</sup> = *v*<sup>*c*</sup>*a*. Indeed, if Bob was honest it
should be that

*g*<sup>*r*</sup> = *g*<sup>*w*</sup><sup>*c*</sup>*g*<sup>*s*</sup> = *u*<sup>*c*</sup>*a*.
 and similarly for *h* with *v*.

**Ex. 3: Proof of cyphertext encryption**

Fix *h* = *g*<sup>*x*</sup> = *P**u**b**K**T* an integer.

-   Public input (*m*, *u*, *v*).
-   Agreed relation
    ((*m*, *u*, *v*),*w*)∈*R* ⇔ *u* = *g*<sup>*w*</sup> ∧ *v* = *g*<sup>*x*</sup><sup>*w*</sup>*m* ⇔ (*u*, *v*)={*m*}<sub>*P**u**b**K**T*</sub>
    under [ ElGamal](/wiki/ElGamalSchnorr "wikilink") with ephemeral key *w*.
-   Private input *w*.
-   Bob will need some random *s* ∈ *Z*<sub>*p*</sub>.
-   Alice will need some random *c* ∈ *Z*<sub>*p*</sub>.

The protocol has three rounds:

*B* → *A* : *a* = *g*<sup>*s*</sup>

*A* → *B* : *c*

*B* → *A* : *r* = *w**c* + *s*
 Alice validates Bob response by checking that
*g*<sup>*r*</sup> = *u*<sup>*c*</sup>*a* and that
*g*<sup>*x*</sup><sup>*r*</sup> = (*v*/*m*)<sup>*c*</sup>*a*. Indeed, if
Bob was honest it should be that

*g*<sup>*r*</sup> = *g*<sup>*w*</sup><sup>*c*</sup>*g*<sup>*s*</sup> = *u*<sup>*c*</sup>*a*.
 and similarly for *h* = *g*<sup>*x*</sup> with *v*′=*v*/*m*.

Composability
-------------

Consider *v*<sub>0</sub>, *v*<sub>1</sub> and
*R*<sub>0</sub>, *R*<sub>1</sub>. Say Bob pretends to have
*w*<sub>0</sub>, *w*<sub>1</sub> such that
(*v*<sub>0</sub>, *w*<sub>0</sub>)∈*R*<sub>0</sub> ∧ (*v*<sub>1</sub>, *w*<sub>1</sub>)∈*R*<sub>1</sub>,
and does not want to disclose them. Is there a Sigma protocol for this
new relation
*R*<sub>0</sub> ∧ *R*<sub>1</sub> = {(*v*<sub>0</sub>, *v*<sub>1</sub>),(*w*<sub>0</sub>, *w*<sub>1</sub>) | (*v*<sub>0</sub>, *w*<sub>0</sub>)∈*R*<sub>0</sub> ∧ (*v*<sub>1</sub>, *w*<sub>1</sub>)∈*R*<sub>1</sub>}?
If there was some for *R*<sub>0</sub> and *R*<sub>1</sub>, then yes. It
suffices to combine the parallel run of both protocols into one, as
tuples.

Now, say Bob pretends to have one of *w*<sub>0</sub> or *w*<sub>1</sub>,
and does not want to disclose it, not tell which one it is. Is there a
Sigma protocol for this new relation
*R*<sub>0</sub> ∨ *R*<sub>1</sub> = {(*v*<sub>0</sub>, *v*<sub>1</sub>),(*w*<sub>0</sub>, *w*<sub>1</sub>) | (*v*<sub>0</sub>, *w*<sub>0</sub>)∈*R*<sub>0</sub> ∨ (*v*<sub>1</sub>, *w*<sub>1</sub>)∈*R*<sub>1</sub>}?
If there was some for *R*<sub>0</sub> and *R*<sub>1</sub>, then
sometimes yes. This sometimes is related to Bob's ability to simulate,
on its own, a valid run of the component Sigma protocols. In other
words, for instance say that Bob does not know *w*<sub>1</sub>, but that
he has the freedom to choose himself the corresponding challenge
*c*<sub>1</sub>. Is he able to efficiently generate
*a*<sub>1</sub>, *c*<sub>1</sub>, *r*<sub>1</sub> so that they are
valid? If so, then yes. This particular property of the component Sigma
protocols is referred to as "existence of a simulator" or "special
honest-verifier zero-knowledge". Here is how.

-   Public input *v*<sub>0</sub>, *v*<sub>1</sub>.
-   Agreed relation *R*<sub>0</sub> ∧ *R*<sub>1</sub>.
-   Private input *w*<sub>0</sub>, say, but could equally be
    *w*<sub>1</sub>.
-   Bob will need some random
    (*u*<sub>0</sub>, *a*<sub>0</sub>)∈*R*<sub>0</sub> and some run
    *a*<sub>1</sub>, *c*<sub>1</sub>, *r*<sub>1</sub>.
-   Alice will need some random *s*.

The protocol has three rounds:

*B* → *A* : (*a*<sub>0</sub>, *a*<sub>1</sub>)

*A* → *B* : *s*

*B* → *A* : (*c*<sub>0</sub>, *c*<sub>1</sub>),(*r*<sub>0</sub>, *r*<sub>1</sub>)
 where *r*<sub>0</sub> is computed by Bob thanks to his knowledge of
*w*<sub>0</sub>. Alice validates Bob response by checking that:

-   *s* = *c*<sub>0</sub> ⊕ *c*<sub>1</sub>
-   *a*<sub>0</sub>, *c*<sub>0</sub>, *r*<sub>0</sub> is valid
-   *a*<sub>1</sub>, *c*<sub>1</sub>, *r*<sub>1</sub> is valid

The intuition is that Bob has "divided up" the random challenge *s* into
*c*<sub>0</sub> which is random, and *c*<sub>1</sub>, which is chosen.
He has passed the challenge *c*<sub>0</sub> thanks to his
*w*<sub>0</sub>. He has passed the challenge *c*<sub>1</sub> because it
was an easy challenge that he has himself chosen.

In the case of the example of the Discrete Logarithm, there exists a
simulator, so that this can be done. Indeed, to generate
*a*<sub>1</sub>, *c*<sub>1</sub>, *r*<sub>1</sub> you:

-   Pick *c*<sub>1</sub>, *r*<sub>1</sub>.
-   Let
    *a*<sub>1</sub> = *g*<sup>*r*<sub>1</sub></sup>*v*<sub>1</sub><sup>−*c*<sub>1</sub></sup>.

Indeed, you then have
*g*<sup>*r*<sub>1</sub></sup> = *v*<sub>1</sub><sup>*c*<sub>1</sub></sup>*a*<sub>1</sub>
so that the run is valid.

Non-interactive version
-----------------------

Instead of doing the Sigma protocol in three rounds, we could just do it
in one round, by musing the Fiat-Shamir heuristics. The idea is that Bob
challenges himself with something that he does not really control,
namely *H*(*a*, *v*), where *H* is a hash function like SHA2. For
instance, let us apply this procedure to the Schnorr identification
protocol. We get:

-   Public input *v* ∈ *G*.
-   Agreed relation (*v*, *w*)∈*R* ⇔ *g*<sup>*w*</sup> = *v*.
-   Private input *w*.
-   Bob will need some random *s* ∈ *Z*<sub>*p*</sub>.
-   Alice will need some random *c* ∈ *Z*<sub>*p*</sub>.

The modified protocol has only one true round, since B' is just B
challenging himself:

*B* → *B*′:*a* = *g*<sup>*s*</sup>

*B*′→*B* : *c* = *H*(*a*, *v*)

*B* → *A* : *a*, *c*, *r* = *w**c* + *s*
 Alice validates Bob response by checking that *c* = *H*(*a*, *v*) and
that *g*<sup>*r*</sup> = *v*<sup>*c*</sup>*a*. Indeed, if Bob was honest
it should be that

*g*<sup>*r*</sup> = *g*<sup>*w*</sup><sup>*c*</sup>*g*<sup>*s*</sup> = *u*<sup>*c*</sup>*a*
.

Now, think of *v* as a message that Bob had to sign. His unique
transmission to Alice

Schnorr signatures
------------------

Bob needs a random ephemeral key *s*. He computes
*c* = *H*(*g*<sup>*s*</sup>, *v*).

  
Bob signs *m* ∈ *G* as
*S**I**G*<sub>*B*</sub>(*m*)=(*g*<sup>*s*</sup>, *c*, *s* + *w**c*).

Alice verifies (*u*, *v*) checking that
*v* = *H*(*g*<sup>*u*</sup>*g*<sup>*w*</sup><sup>*v*</sup>, *v*).

Indeed, if Bob was honest it should be that
*g*<sup>*u*</sup>*g*<sup>*x*</sup><sup>*v*</sup> = *g*<sup>*s* + *w**c*</sup>*g*<sup>*w*</sup><sup>*c*</sup> = *g*<sup>*s*</sup>.


