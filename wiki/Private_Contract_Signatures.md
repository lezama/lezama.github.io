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

An SPCS<sub>*S*</sub>(*m*) is

NI(⋁<sub>*i* ∈ *S*</sub>CCE<sup>*T*</sup>(*H*(*m*),(Pub<sup>*P*<sub>*i*</sub></sup>,*v*)))(*g*<sup>*s*</sup>, *H*(*g*<sup>*s*</sup>, *m*))
 with s random. Intuitively:

-   It constitutes a proof that
    *v* = {*H*(*m*)}<sub>Pub<sup>*T*</sup></sub> under
    [ElGamal](/wiki/ElGamal "wikilink").
-   In order to provide such a proof one needs to have the ephemeral
    key used.
-   It also constitutes a proof that the ephemeral key was one of
    {Priv<sup>*P*<sub>*i*</sub></sup>}<sub>*i* ∈ *S*</sub>.
-   Thus, whoever has done it, has admittedly signed m.
-   But in order to which *P*<sub>*i*</sub> has signed, one needs a
    proof of which of private keys was used.

To unravel it, means to convert SPCS<sub>*S*</sub>(*m*) into the final
signature SIG<sub>*i* ∈ *S*</sub>(*m*):

NI(CCE<sup>*T*</sup>(*H*(*m*),(Pub<sup>*P*<sub>*i*</sub></sup>,*v*))∨CCD<sup>*T*</sup>(*H*(*m*),(Pub<sup>*P*<sub>*i*</sub></sup>,*v*)))(*g*<sup>*s*′</sup>, *H*(*g*<sup>*s*′</sup>, *m*))
 with s' random. Intuitively:

-   In order to accomplish the conversion one needs to either have
    Priv<sub>*P*<sub>*i*</sub></sub> used as ephemeral key, or to have
    Priv<sub>*T*</sub>.
-   It constitutes a proof that
    *v* = {*H*(*m*)}<sub>Pub<sup>*T*</sup></sub> under
    [ElGamal](/wiki/ElGamal "wikilink") with ephemeral key
    Priv<sub>*P*<sub>*i*</sub></sub>, which amounts to *P*<sub>*i*</sub>
    signing m..
-   No step discloses Priv<sub>*P*<sub>*i*</sub></sub>.

Standard scheme
---------------

Normally, a PCS<sub>*B*</sub><sup>*A*</sup>(*m*) is

NI((CCE<sup>*T*</sup>(0,*n*)∧Schnorr<sub>*B*</sub>)∨(CCE<sup>*T*</sup>(1,*n*)∧Schnorr<sub>*A*</sub>))(*g*<sup>*s*</sup>, *H*(*g*<sup>*s*</sup>, *m*))
 with s random.

To do
-----

Check duplication of a and c in and and or constructs.

Check whether non-interactive CCE under ephemeral key PubB and challenge
m is an established way of signing.

Give simulators for CCE and CCT.
