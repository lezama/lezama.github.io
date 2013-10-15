---
title: Private Contract Signatures
permalink: wiki/Private_Contract_Signatures/
layout: wiki
---

Private Contract Signatures are a cryptography primitive which we need
for the [Secure Contract Signing
Protocol](/wiki/Secure_Contract_Signing_Protocol "wikilink").

Those are constructed via non-interactive zero-knowledge proofs
constructions, and based upon the [Decisional
Diffie-Hellman](http://en.wikipedia.org/wiki/Decisional_Diffie%E2%80%93Hellman_assumption)
assumption.

It was introduced in [Abuse-free optimistic contract
signing](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.118.4142)
by Garay, Jakobsson, MacKenzie (1999). Comment on the usefulness of this
paper to the project [here](/wiki/GarayJakobssonMackenzie "wikilink").

This page aims to give an outline of how they work, and how to implement
them.

Some Cryptography
-----------------

The following must be understood first. In particular, the description
of PCS we give uses the notations introduced there.

Outline of [ElGamal encryption](/wiki/ElGamalSchnorr "wikilink"), which are
encryption and signature schemes.

Outline of [Sigma protocols](/wiki/Sigma_Protocols "wikilink"), which are
composable, interactive zero-knowledge proof schemes.

Scheme
------

PCS<sub>*B*</sub><sup>*A*</sup>(*m*)=((CCE<sup>*T*</sup>(0,*n*)∧Schnorr<sub>*B*</sub>)∨(CCE<sup>*T*</sup>(1,*n*)∧Schnorr<sub>*A*</sub>))(*H*(*g*<sup>*s*</sup>, *m*))
 with s random.

Why not try

$$\\textrm{PCS}\_B^A(m)=\\left(\\textrm{CCE}^T(\\textrm{Pub}^A,(\\textrm{Pub}^B,v))\\vee\\textrm{CCE}^T(\\textrm{Pub}^B,(g^{\\textrm{Pub}^A,v))\\right)(H(g^s,m))$$
 with s random?
