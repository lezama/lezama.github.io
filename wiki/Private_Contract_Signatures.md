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

Simplified scheme
-----------------

An SPCS<sub>*B*</sub><sup>*A*</sup>(*m*) is

NI(CCE<sup>*T*</sup>(*m*,(Pub<sup>*B*</sup>,*v*))∨CCE<sup>*T*</sup>(*m*,(Pub<sup>*A*</sup>,*v*)))(*g*<sup>*s*</sup>, *H*(*g*<sup>*s*</sup>, *m*))
 with s random.

To unravel it, we need USPCS<sub>*B*</sub><sup>*A*</sup>(*m*)

NI(CCE<sup>*T*</sup>(*m*,(Pub<sup>*B*</sup>,*v*))∨CCD<sup>*T*</sup>(*m*,(Pub<sup>*B*</sup>,*v*)))(*g*<sup>*s*</sup>, *H*(*g*<sup>*s*</sup>, *m*))
 with s random.

A signature SIG<sub>*B*</sub><sup>*A*</sup>(*m*) is a pair

SPCS<sub>*B*</sub><sup>*A*</sup>(*m*),USPCS<sub>*B*</sub><sup>*A*</sup>(*m*).

Normal scheme
-------------

Normally, a PCS<sub>*B*</sub><sup>*A*</sup>(*m*) is

NI((CCE<sup>*T*</sup>(0,*n*)∧Schnorr<sub>*B*</sub>)∨(CCE<sup>*T*</sup>(1,*n*)∧Schnorr<sub>*A*</sub>))(*g*<sup>*s*</sup>, *H*(*g*<sup>*s*</sup>, *m*))
 with s random.

To do
-----

Check duplication of a and c in and and or constructs.

Check whether non-interactive CCE under ephemeral key PubB and challenge
m is an established way of signing.

Give simulators for CCE and CCT.
