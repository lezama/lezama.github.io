---
title: AsokanSchunter
permalink: wiki/AsokanSchunter/
layout: wiki
---

The link does not grant access to the whole document, however I
recovered it. This is a recent review paper by specialists, hence a good
entry to the topic. The comments here are biased towards SXP.

Fair Exchange
-------------

Describes fair exchange protocols as ways to exchange things between
distrustful parties in such a way that either both parties receive what
they expect or neither parties does. Includes receipts for payments,
certified mail, and contract signatures more specfically.

Types of Fair Exchanges (FX)
----------------------------

### With a Trusted Third Party (TTP)

Requires a referee. In the setting of SXP, maybe the market could maybe
play such a role, but this is costly.

The protocols that implement this have a simple common pattern. Alice
(A) and Bob (B) need to sign contract (C) with there private keys
PrivKA/PrivKB, Trent (T) is the Trusted Third Party. See
[here](http://en.wikipedia.org/wiki/Security_protocol_notation) for the
notation.

*A* → *B* : {{*C*}<sub>*P**r**i**v**K**A*</sub>}<sub>*K*</sub>

*A* → *T* : *K*

*B* → *T* : {{*C*}<sub>*P**r**i**v**K**A*</sub>}<sub>*K*</sub>, {*C*}<sub>*P**r**i**v**K**B*</sub> : &lt;*m**a**t**h* &gt; *T* → *B* : *K*

*T* → *A* : {*C*}<sub>*P**r**i**v**K**B*</sub>

To be honest I am not sure why going through K is necessary, this looks
like an optimization for Digital Certified Mail. In the explanations all
this seems to boil down to the boring protocol:

*A* → *T* : {*C*}<sub>*P**r**i**v**K**A*</sub>

*B* → *T* : {*C*}<sub>*P**r**i**v**K**B*</sub>

*T* → *A* : {*C*}<sub>*P**r**i**v**K**B*</sub>

*T* → *B* : {*C*}<sub>*P**r**i**v**K**A*</sub>

### Being Optimistic

Does not require a referee, unless there is a conflict.

#### Optimistic FX

#### Verifiable escrow of digital signatures

#### Verifiable escrow using pre-issued coupons

### Exchanging in parts

Questions on this paper
-----------------------

Why not go for the following natural solutions: the contract C wears the
mention "This contract is not valid if not signed by PubKA, and then by
PubKB by time t". This way Alice can safely sign it with PrivB and send
it to Bob. Bob may not sign it but then the contract is not valid. To
validate he must sign it and have it time-stamped by time t... OK maybe
there would be two problems:

-   Alice is not ensured to get her copy of the valid contract;
-   The time-stamping service would need to be solicited all
    too frequently.

