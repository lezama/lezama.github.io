---
title: Sigma Protocols
permalink: wiki/Sigma_Protocols/
layout: wiki
---

Those are key to understanding [Private Contract
Signatures](/wiki/Private_Contract_Signatures "wikilink").

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

Examples
--------

Here are examples of Sigma protocols based on the hardness of Discrete
Logarithms. Fix *p* a prime and *g* an integer. The powers of *g* form a
subgroup *G* inside the group *Z*<sub>*p*</sub>, which is that of
integers modulo *p*. The choice of these *p* and *g* is important so
that they meet the [Decisional
Diffie-Hellman](http://en.wikipedia.org/wiki/Decisional_Diffie%E2%80%93Hellman_assumption)
assumption; but there are standard techniques for doing that.

**Ex. 1: Schnorr identification protocol**

Fix *g* an integer.

-   Public input *v* = Pub<sub>*B*</sub>.
-   Agreed relation (*v*, *w*)∈*R* ⇔ *g*<sup>*w*</sup> = *v*.
-   Private input *w* = Priv<sub>*B*</sub>.
-   Bob will need some random ephemeral *s* ∈ *Z*<sub>*p*</sub>.
-   Alice will need some random *c* ∈ *Z*<sub>*p*</sub>.

The protocol has three rounds:

*B* → *A* : *a* = *g*<sup>*s*</sup>

*A* → *B* : *c*

*B* → *A* : *r* = *w**c* + *s*
 Alice validates Bob's response by checking that
*g*<sup>*r*</sup> = *v*<sup>*c*</sup>*a*. Indeed, if Bob was honest it
should be that

*g*<sup>*r*</sup> = *g*<sup>*w*</sup><sup>*c*</sup>*g*<sup>*s*</sup> = *v*<sup>*c*</sup>*a*
 **Denote by Schnorr<sub>*B*</sub>(*c*) a run of this protocol by prover
B under challenge c.**

**Ex. 2: Diffie-Hellman pairs**

Fix *g* and *h* integers. The powers of *h* form a subgroup *H* inside
the group *Z*<sub>*p*</sub>.

-   Public input *u* ∈ *G*, *v* ∈ *H*.
-   Agreed relation
    ((*u*, *v*),*w*)∈*R* ⇔ *g*<sup>*w*</sup> = *u* ∧ *h*<sup>*w*</sup> = *v*.
-   Private input *w*.
-   Bob will need some random *s* ∈ *Z*<sub>*p*</sub>.
-   Alice will need some random *c* ∈ *Z*<sub>*p*</sub>.

The protocol has three rounds:

*B* → *A* : *a* = *g*<sup>*s*</sup>, *a*′=*g*<sup>*s*′</sup>

*A* → *B* : *c*, *c*′

*B* → *A* : *r* = *w**c* + *s*, *r*′=*w**c*′+*s*′
 Alice validates Bob's response by checking that
*g*<sup>*r*</sup> = *u*<sup>*c*</sup>*a* and that
*h*<sup>*r*′</sup> = *v*<sup>*c*′</sup>*a*′. Indeed, if Bob was honest
it should be that

*g*<sup>*r*</sup> = *g*<sup>*w*</sup><sup>*c*</sup>*g*<sup>*s*</sup> = *u*<sup>*c*</sup>*a*.
 and similarly for *h* with *v*.

**Ex. 3: Proof of cyphertext content by encrypter**

Fix *g* and *h* = *g*<sup>*x*</sup> = Pub<sub>*T*</sub> integers.

-   Public input *m* and *m*′=(*u*, *v*).
-   Agreed relation
    ((*m*, (*u*, *v*)), *w*)∈*R* ⇔ *u* = *g*<sup>*w*</sup> ∧ *v* = *g*<sup>*x*</sup><sup>*w*</sup>*m* ⇔ (*u*, *v*)={*m*}<sub>Pub<sub>*T*</sub></sub>
    under [ ElGamal](/wiki/ElGamalSchnorr "wikilink") with ephemeral key *w*.
-   Private input *w*.
-   Bob will need some random *s* ∈ *Z*<sub>*p*</sub>.
-   Alice will need some random *c* ∈ *Z*<sub>*p*</sub>.

The protocol has three rounds:

*B* → *A* : *a* = *g*<sup>*s*</sup>, *a* = *g*<sup>*x*</sup><sup>*s*</sup>

*A* → *B* : *c*

*B* → *A* : *r* = *w**c* + *s*, *r* = *w**c* + *s*
 Alice validates Bob's response by checking that
*g*<sup>*r*</sup> = *u*<sup>*c*</sup>*a* and that
*g*<sup>*x*</sup><sup>*r*</sup> = (*v*/*m*)<sup>*c*</sup>*a*′. Indeed,
if Bob was honest it should be that

*g*<sup>*r*</sup> = *g*<sup>*w*</sup><sup>*c*</sup>*g*<sup>*s*</sup> = *u*<sup>*c*</sup>*a*.
 and similarly for *h* = *g*<sup>*x*</sup> with *v*′=*v*/*m*.

**Denote by CCE<sub>*T*</sub>(*m*, *m*′)(*c*) a run of this protocol
under challenge c.**

**Ex. 4: Proof of cyphertext content by decrypter**

Fix *g* and *h* = *g*<sup>*x*</sup> = Pub<sub>*T*</sub> integers.

-   Public input *m* and *m*′=(*u*, *v*).
-   Agreed relation
    ((*m*, (*u*, *v*)), *w*)∈*R* ⇔ *v* = *u*<sup>*x*</sup>*m* ⇔ (*u*, *v*)={*m*}<sub>Pub<sub>*T*</sub></sub>
    under [ ElGamal](/wiki/ElGamalSchnorr "wikilink") for Trent.
-   Private input *x* = Priv<sub>*T*</sub>.
-   Trent will need some random *s* ∈ *Z*<sub>*p*</sub>.
-   Alice will need some random *c* ∈ *Z*<sub>*p*</sub>.

The protocol has three rounds:

*T* → *A* : *a* = *g*<sup>*s*</sup>, *a*′=*u*<sup>*s*′</sup>

*A* → *T* : *c*

*T* → *A* : *r* = *x**c* + *s*
 Alice validates Trent's response by checking that
*g*<sup>*r*</sup> = *h*<sup>*c*</sup>*a* and that
*u*<sup>*r*</sup> = (*v*/*m*)<sup>*c*</sup>*a*′. Indeed, if Bob was
honest it should be that

*g*<sup>*r*</sup> = *g*<sup>*x*</sup><sup>*c*</sup>*g*<sup>*s*</sup> = *h*<sup>*c*</sup>*a*.
 and

*u*<sup>*r*</sup> = *u*<sup>*x**c*</sup>*u*<sup>*s*</sup> = (*v*/*m*)<sup>*c*</sup>*a*′.

**Denote by CCD<sub>*T*</sub>(*m*, *m*′)(*c*) a run of this protocol
under challenge c.**

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
tuples. We can use the same challenge c for both runs.

**Denote by (*P* ∧ *Q*)(*c*) the and composition of two protocols
*P*(*c*) and *Q*(*c*).**

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
-   Alice will need some random *c*.

The protocol has three rounds:

*B* → *A* : (*a*<sub>0</sub>, *a*<sub>1</sub>)

*A* → *B* : *s*

*B* → *A* : (*c*<sub>0</sub>, *c*<sub>1</sub>),(*r*<sub>0</sub>, *r*<sub>1</sub>)
 where *r*<sub>0</sub> is computed by Bob thanks to his knowledge of
*w*<sub>0</sub>. Alice validates Bob response by checking that:

-   *c* = *c*<sub>0</sub> ⊕ *c*<sub>1</sub>
-   *a*<sub>0</sub>, *c*<sub>0</sub>, *r*<sub>0</sub> is valid
-   *a*<sub>1</sub>, *c*<sub>1</sub>, *r*<sub>1</sub> is valid

The intuition is that Bob has "divided up" the random challenge *s* into
*c*<sub>0</sub> which is random, and *c*<sub>1</sub>, which is chosen.
He has passed the challenge *c*<sub>0</sub> thanks to his
*w*<sub>0</sub>. He has passed the challenge *c*<sub>1</sub> because it
was an easy challenge that he has himself chosen.

In the case of Schnorr<sub>*B*</sub>, there exists a simulator, so that
this can be done. Indeed, to generate
*a*<sub>1</sub>, *c*<sub>1</sub>, *r*<sub>1</sub> you:

-   Pick *c*<sub>1</sub>, *r*<sub>1</sub>.
-   Let
    *a*<sub>1</sub> = *g*<sup>*r*<sub>1</sub></sup>*v*<sub>1</sub><sup>−*c*<sub>1</sub></sup>.

Indeed, you then have
*g*<sup>*r*<sub>1</sub></sup> = *v*<sub>1</sub><sup>*c*<sub>1</sub></sup>*a*<sub>1</sub>
so that the run is valid.

**Denote by (*P* ∨ *Q*)(*c*) the or composition of two protocols P and
Q, under the divided up challenge c.**

Non-interactive version
-----------------------

Instead of doing the Sigma protocol in three rounds, we could just do it
in one round, by musing the Fiat-Shamir heuristics. The idea is that Bob
challenges himself with something that he does not really control,
namely *H*(*a*, *v*), where *H* is a hash function like SHA2. For
instance, let us apply this procedure to the Schnorr identification
protocol. We get:

-   Public input *m* = *v* ∈ *G*.
-   Agreed relation (*v*, *w*)∈*R* ⇔ *g*<sup>*w*</sup> = *v*.
-   Private input *w*.
-   Bob will need some random *s* ∈ *Z*<sub>*p*</sub>.

The modified protocol has only one true round, since B' is just B
challenging himself:

*B* → *B*′:*a* = *g*<sup>*s*</sup>

*B*′→*B* : *c* = *H*(*a*, *m*)

*B* → *A* : *a*, *c*, *r* = *w**c* + *s*
 Alice validates Bob response by checking that *c* = *H*(*a*, *m*) and
that *v*<sup>−*c*</sup>*g*<sup>*r*</sup> = *a*. Indeed, if Bob was
honest it should be that

*v*<sup>−*c*</sup>*g*<sup>*r*</sup> = *g*<sup>−*w**c*</sup>*g*<sup>*w**c*</sup>*g*<sup>*s*</sup> = *a*
.

Schnorr signatures
------------------

Let us further modify the above, and say that the challenge that Bob
will put to himself is to be fabricated based upon some public *m*
instead of *v*.

-   Public input *m* a message and *v* = *P**u**b**K**B*.
-   Agreed relation (*v*, *w*)∈*R* ⇔ *g*<sup>*w*</sup> = *v*.
-   Private input *w* = *P**r**i**v**K**B*.
-   Bob will need some random ephemeral *s* ∈ *Z*<sub>*p*</sub>.

  
Bob computes *c* = *H*(*g*<sup>*s*</sup>, *m*) and *r* = *s* + *w**c*.

Bob signs *m* ∈ *G* as *S**I**G*<sub>*B*</sub>(*m*)=(*c*, *r*).

Alice verifies (*c*, *r*) checking that *c* = *H*(*a*, *m*) with
*a* = *v*<sup>−*c*</sup>*g*<sup>*r*</sup>.

Indeed, if Bob was honest it should be that
*v*<sup>−*c*</sup>*g*<sup>*r*</sup> = *g*<sup>−*w**c*</sup>*g*<sup>*w**c* + *s*</sup> = *g*<sup>*s*</sup> = *a*.


