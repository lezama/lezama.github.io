---
title: Private Contract Signatures
permalink: wiki/Private_Contract_Signatures/
layout: wiki
---

Private Contract Signatures are a cryptography primitive which we need
for the [Secure Contract Signing
Protocol](/wiki/Secure_Contract_Signing_Protocol "wikilink").

It was introduced in [Abuse-free optimistic contract
signing](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.118.4142)
by Garay, Jakobsson, MacKenzie (1999).

This page aims to give an outline of what they achieve, and how to
implement them.

Specifications
--------------

SPCS<sub>*S*</sub><sup>*T*</sup>(*m*) denotes a Private Contract
Signatures by Pi in S on contract m with Trusted Third Party T. The
object is such that:

-   It can be created any of the Pi's in S and, in the eyes of an
    external party, faked by any other of the Pj's in S;
-   The creating Pi, or T, are able to convert it into
    SIG<sub>*i*</sub><sup>*T*</sup>(*m*), and other Pj's can be
    convinced of this.

Some Cryptography
-----------------

The following must be understood first. In particular, the description
of PCS we give uses the notations introduced there.

Outline of [ElGamal encryption](/wiki/ElGamalSchnorr "wikilink"), which are
encryption and signature schemes.

Outline of [Sigma protocols](/wiki/Sigma_Protocols "wikilink"), which are
composable, interactive zero-knowledge proof schemes.

Standard scheme
---------------

A **private contract signature** PCS<sub>*S*</sub>(*m*, *n*) is

NI(⋁<sub>*i* ∈ *S*</sub>(CCE<sup>*T*</sup>(*i*,*n*)∧Schnorr<sub>*i*</sub>))(*g*<sup>*s*</sup>, *H*(*g*<sup>*s*</sup>, *m*))
 with s random. Intuitively:

-   It constitutes a proof that one of the Pi has passed the Schnorr
    identification test on challenge *H*(*g*<sup>*s*</sup>, *m*).
-   This amounts to having signed *m*, just like in the Schnorr
    signature scheme.
-   Except that we do not know, yet, which of the *P*<sub>*i*</sub>
    has signed.
-   In order to convert this into a signature by *P*<sub>*i*</sub>, one
    must prove that the cyphertext *n* has content the integer *i*.

A **private contract signature revealer** RPCS<sub>*i*</sub>(*n*) is

NI(CCE<sup>*T*</sup>(*i*,*n*)∨CCD<sup>*T*</sup>(*i*,*n*))(*g*<sup>*s*</sup>, *H*(*g*<sup>*s*</sup>, *m*))
 with s random. Intuitively:

-   It constitutes a proof that the cyphertext *n* has content the
    integer *i*.
-   Either *P*<sub>*i*</sub> or *T* can produce this.

A **contract signature** SIG<sub>*i*</sub>(*m*) is

(PCS<sub>*S*</sub>(*m*,*n*),RPCS<sub>*i*</sub>(*n*))
 Intuitively:

-   It constitutes a combined proof that Pi has passed the Schnorr
    identification test on challenge *H*(*g*<sup>*s*</sup>, *m*).
-   This amounts to having signed *m*, just like in the Schnorr
    signature scheme.

Simplified scheme (Failed attempt)
----------------------------------

An SPCS<sub>*S*</sub><sup>*T*</sup>(*m*) is

NI(⋁<sub>*i* ∈ *S*</sub>CCE<sup>*T*</sup>(*H*(*m*),(Pub<sup>*P*<sub>*i*</sub></sup>,*v*)))(*g*<sup>*s*</sup>, *H*(*g*<sup>*s*</sup>, *m*))
 with s random. Intuitively:

-   It constitutes a proof that
    *v* = {*H*(*m*)}<sub>Pub<sup>*T*</sup></sub> under
    [ElGamal](/wiki/ElGamal "wikilink"), with ephemeral key one of
    {Priv<sup>*P*<sub>*i*</sub></sup>}<sub>*i* ∈ *S*</sub>.
-   In order to provide such a proof one needs to have the ephemeral
    key used.
-   Thus, whoever has done it, has admittedly signed m.
-   But in order to know which of the *P*<sub>*i*</sub> has signed, one
    needs a proof of which of private keys was used.

To unravel it, means to convert SPCS<sub>*S*</sub><sup>*T*</sup>(*m*)
into the final signature SIG<sub>*i* ∈ *S*</sub><sup>*T*</sup>(*m*):

NI(CCE<sup>*T*</sup>(*H*(*m*),(Pub<sup>*P*<sub>*i*</sub></sup>,*v*))∨CCD<sup>*T*</sup>(*H*(*m*),(Pub<sup>*P*<sub>*i*</sub></sup>,*v*)))(*g*<sup>*s*′</sup>, *H*(*g*<sup>*s*′</sup>, *m*))
 with s' random. Intuitively:

-   In order to accomplish the conversion one needs to either have
    Priv<sub>*P*<sub>*i*</sub></sub> used as ephemeral key, or to have
    Priv<sub>*T*</sub>.
-   It constitutes a proof that
    *v* = {*H*(*m*)}<sub>Pub<sup>*T*</sup></sub> under
    [ElGamal](/wiki/ElGamal "wikilink") with ephemeral key
    Priv<sub>*P*<sub>*i*</sub></sub>, which amounts to *P*<sub>*i*</sub>
    signing m.
-   No step discloses Priv<sub>*P*<sub>*i*</sub></sub>.

This scheme is simpler than the original scheme. It has dangerous
weaknesses, however:

-   By requiring that Priv<sub>*P*<sub>*i*</sub></sub> be the ephemeral
    key for ElGamal encryption, we are imposing that the pairs
    (Priv<sub>*P*<sub>*i*</sub></sub>, Pub<sup>*P*<sub>*i*</sub></sup>)
    and (Priv<sub>*T*</sub>, Pub<sup>*T*</sup>) are based on the same
    Diffie-Hellman group. Altogether, this would mean that all pairs get
    generates with respect to the same group. This is non-traditional,
    and perhaps it weakens security? Nevertheless, notice that precise,
    fixed groups have been recommended for use, for instance in [RFC
    5114](http://tools.ietf.org/html/rfc5114#page-4).
-   The same ephemeral key Priv<sub>*P*<sub>*i*</sub></sub> is reused
    over and over, which means that the cyphertext is always
    *H*(*m*)*g*<sup>Priv<sub>*P*<sub>*i*</sub></sub>Priv<sub>*T*</sub></sup>
    but since *H*(*m*) is known, so is
    *g*<sup>Priv<sub>*P*<sub>*i*</sub></sub>Priv<sub>*T*</sub></sup>,
    and so the next time Pi is immediately identified as the creator of
    the SPCS.
-   Worse even, Pi's signature, once it has been used once, can then be
    forged, since signing amounts to multiply by
    *g*<sup>Priv<sub>*P*<sub>*i*</sub></sub>Priv<sub>*T*</sub></sup> in
    this scheme.

To do
-----

Check duplication of a and c in and and or constructs.

Give simulators for CCE and CCT.
