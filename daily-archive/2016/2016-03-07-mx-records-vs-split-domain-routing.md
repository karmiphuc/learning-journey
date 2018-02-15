---
layout: post
summary: "TL;DR: MX Records are used to mitigate risks, SDR used for "
tags: server programming
---
### MX Record

![](http://www.telnetport25.com/legacySites/msex/MX-2MX.jpg)

![](http://cfile5.uf.tistory.com/image/1479CC454F83D0B313972B)

### Split Domain Routing

1. qmail: [https://qmail.jms1.net/multi-location.shtml](https://qmail.jms1.net/multi-location.shtml)
> New York - 10.1.1.1	| Atlanta - 10.2.2.2 | Denver - 10.3.3.3
> --- | --- | ---
> Nick <nick@megacorp.xyz> | Alex <alex@megacorp.xyz> | Dave <dave@megacorp.xyz>
> Nancy <nancy@megacorp.xyz> | Alice <alice@megacorp.xyz>	| Diane <diane@megacorp.xyz>

2. SDR case: [https://luxsci.com/blog/split-domain-routing-getting-email-for-your-domain-at-two-providers.html](https://luxsci.com/blog/split-domain-routing-getting-email-for-your-domain-at-two-providers.html)
> Here is how it is set up:
>
>1. The DNS MX records for my-doctors-on-call.com will remain pointing to the inbound email servers of Company X
>2. LuxSci.com will setup a “subdomain” called “sdr.my-doctors-on-call.com” on its email system and configure it as a “domain alias” whereby any email that arrives for “emily@sdr.my-doctors-on-call.com” is merely delivered on LuxSci to emily@my-doctors-on-call.com”.
>3. DNS MX records for sdr.my-doctors-on-call.com will be created and these will point to LuxSci’s inbound email servers.
>4. The customer will create email forwarding rules in company X so that any inbound email messages that arrive at Company X for any users that want to get their email at LuxSci.com now are forwarded to those user’s addresses @sdr.my-doctors-on-call.com.  For example,  the customer would create a rule so that email to emily@my-doctors-on-call.com is forwarded to emily@sdr.my-doctors-on-call.com
>5. As more users are migrated to LuxSci.com and ready to use email there, similar forwarding rules are created.
>6. Once everyone is migrated to LuxSci.com, the DNS MX records for my-doctors-on-call.com itself can be updated so that email is delivered directly to LuxSci.com, the subdomain can be deleted, and the account with provider X can be closed.
>
>![](https://luxsci-public.s3.amazonaws.com/s3/blog/sdr.gif)
