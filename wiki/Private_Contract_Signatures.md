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

Simplified scheme
-----------------

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

This scheme is simpler than the original scheme. It has a drawback,
however. Indeed, by requiring that Priv<sub>*P*<sub>*i*</sub></sub> be
the ephemeral key for El Gammal encryption, we are imposing that the
pairs
(Priv<sub>*P*<sub>*i*</sub></sub>, Pub<sup>*P*<sub>*i*</sub></sup>) and
(Priv<sub>*T*</sub>, Pub<sup>*T*</sup>) are based on the same
Diffie-Hellman group. Altogether, this would mean that all pairs get
generates with respect to the same group. This is non-traditional, and
perhaps it weakens security? Nevertheless, notice that precise, fixed
groups have been recommended for use, for instance in [RFC
5114](http://tools.ietf.org/html/rfc5114#page-4).

Standard scheme
---------------

Normally, a PCS<sub>*B*</sub><sup>*A*</sup>(*m*) is

NI((CCE<sup>*T*</sup>(0,*n*)∧Schnorr<sub>*B*</sub>)∨(CCE<sup>*T*</sup>(1,*n*)∧Schnorr<sub>*A*</sub>))(*g*<sup>*s*</sup>, *H*(*g*<sup>*s*</sup>, *m*))
 with s random.

To do
-----

There might be a pb with g having to be the same in Trent's and the
Party's for the simplified scheme to work.

Check duplication of a and c in and and or constructs.

Check whether non-interactive CCE under ephemeral key PubB and challenge
m is an established way of signing.

Give simulators for CCE and CCT.
