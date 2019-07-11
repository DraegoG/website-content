---
title: What is an RFC?
description: "RFCs, Request for Comments, are publications from the technology community"
date: 2018-10-03T07:00:00+02:00
tags: network
---

In several blog posts I mention "this technology is defined in RFC xxxx", or "see RFC yyyy for the nitty gritty details".

What is an RFC?

RFC stands for _Request for Comments_. You might have RFC in various environments now, but traditionally what we mean with RFC on the Internet is a publication that's written by engineers and computer scientists, aimed at other professionals that work in the Internet sphere.

RFCs have a long history, starting back in 1969 in ARPANET times. The Internet was created in this way, with RFCs being starting point of discussion, or protocol implementation details that people used to implement the actual software.

The name, Request for Comments, encouraged a community discussion around those papers, that originally circulated in printed form.

RFCs today, before being added as official RFCs, go through various steps, that might take many months or years of discussions. This is because an RFC today, once published, cannot be changed any more. The entire process is managed by IETF, the _Internet Engineering Task Force_.

Revisions to RFC documents need to be published as independent RFCs, and older RFCs are marked as superseded by those newer revisions. Other RFC supplement what older RFC specify.

For example, RFC 1349 from 1992, titled "_Type of Service in the Internet Protocol Suite_", was obsoleted by RFC 2474 in 1998, titled "_Definition of the Differentiated Services Field (DS Field) in the IPv4 and IPv6 Headers_".

Here are some very famous RFC documents that are very well worth the read. Those are things that will be relevant for a long time (I myself printed some of them back in high school like 20 years ago, and I still have those), and are the foundation of the Internet:

- [RFC 791: IP](https://tools.ietf.org/html/rfc791)
- [RFC 793: TCP](https://tools.ietf.org/html/rfc793)
- [RFC 1034: DNS](https://tools.ietf.org/html/rfc1034)
- [RFC 4291: IPv6](https://tools.ietf.org/html/rfc4291)
- [RFC 6749: OAuth 2.0](https://tools.ietf.org/html/rfc6749)

Some other RFCs are less technical, like [RFC 1855 Netiquette Guidelines](https://tools.ietf.org/html/rfc1855), and some others are just funny jokes by engineers for engineers, like [RFC 2324](https://tools.ietf.org/html/rfc2324), the _Hyper Text Coffee Pot Control Protocol_.

So, in conclusion: RFCs are technical documents that, after going through a rigorous process of discussion and technical verification are added to the list of official protocols recognized by the IETF, and being a standard they can then be implemented by software vendors.