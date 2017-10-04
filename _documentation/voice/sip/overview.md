---
title: Overview
description: Use Nexmo SIP to forward inbound and send outbound Voice calls that use the Session Initiation Protocol.
---

# SIP Overview

Nexmo allows you to [forward inbound](#forward-inbound) and [send outbound](#sip-outbound) Voice calls using the [Session Initiation Protocol](https://en.wikipedia.org/wiki/Session_Initiation_Protocol).

This document explains the relevant setup options.

**Endpoint**

You can send your [INVITE](https://en.wikipedia.org/wiki/List_of_SIP_request_methods) requests to the Nexmo SIP endpoint: `sip.nexmo.com`.

**Authentication**

Every INVITE request is authenticated with Digest authentication:

- `username` - your Nexmo *key*
- `password` - your Nexmo *secret*

**Service records**

If your system is not enabled for [Service records](https://en.wikipedia.org/wiki/SRV_record) (SRV records), you should load balance between the two closest endpoints and set the remaining ones as backup. The Nexmo SIP endpoints are:

- `sip-us1.nexmo.com` (Washington)
- `sip-us2.nexmo.com` (Washington)
- `sip-eu1.nexmo.com` (London)
- `sip-eu2.nexmo.com` (London)
- `sip-ap1.nexmo.com` (Singapore)
- `sip-ap2.nexmo.com` (Singapore)

**Recipient**

Recipient numbers must be in [E.164](https://en.wikipedia.org/wiki/E.164) format: `country code+area code+local code+extension`.

For example, the phone number 331908817135 is made up of:

* country code (CC): 33
* area code (AC): 1908
* local code (LC): 8
* extension: 17135

**Caller ID**

Set the Caller Line Identity (CLI) in the *From* header using E.164. For example: `From: <sip:447937947990@sip.nexmo.com>`.

**Codecs**

The following codecs are supported:

- PCMA (G711a)
- PCMU (G711u)
- iLBC
- g729 (without annexb)
- g722
- Speex16

**Media traffic**

The list of IPs/subnets is subject to change. Rather than white-listing specific subnets, open traffic from all IP ranges to port range `10000:20000`.

**DTMF**

Nexmo supports out-of-band DTMF. For more information, see [RFC2833](https://www.ietf.org/rfc/rfc2833.txt).

**Health checks**

Use the OOD [OPTIONS](https://en.wikipedia.org/wiki/List_of_SIP_request_methods) method to run a health check on our SIP trunks.

**Protocols**

You can use the following protocols:

- UDP on port 5060
- TCP on port 5060
- TLS on port 5061

[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is a cryptographic protocol designed to provide communications security to your SIP connection. You can use self-signed certificates on your user agent, Nexmo does not validate the certificate on the client side.

Connections using TLS 1.0 or more recent are accepted. Older protocols are disabled as they are considered insecure.

## Inbound configuration

This section tells you how to:

- [Configure your system for SIP forwarding](#configure-your-system-for-sip-forwarding)
- [Configure example servers](#configure-example-servers)

## Configuring your system for SIP forwarding

To configure for SIP forwarding:

1. Sign into [Dashboard](https://dashboard.nexmo.com/sign-in).
2. In Dashboard, click *Products* > *Numbers*.
3. Scroll to the number to forward from, then select *Forward to SIP*.
4. Type a valid SIP URI and click *Update*. For example 1234567890@mydomain.com.
  This field supports comma-separated entries for failover capabilities. For example: `1234567890@mydomain.com, 1234567890@my2domain.com, 1234567890@my3domain.com`. If you set more than one endpoint in *Forward to SIP* the call is initially forwarded to the first endpoint in the list. If this fails, the call is forwarded to the second endpoint in the list, and so on.
  Calls failover for the whole 5xx class of HTTP errors. The timeout is 486.
5. Ensure that the traffic generated from the following IP addresses can pass your firewall:

  * 173.193.199.24
  * 174.37.245.34
  * 5.10.112.121
  * 5.10.112.122
  * 119.81.44.6
  * 119.81.44.7

> **Note**: Nexmo supports TLS on inbound connections. To enable this, enter a valid secure URI in the format sips:user@(IP|domain). For example, *sips:1234567890@mydomain.com*. By default, traffic is sent to port 5061. To use a different port, add it at the end of your URI: *sips:1234567890@mydomain.com:5062*.

## Example configurations

We have provided examples for a number of different SIP systems:

* [Asterisk](/voice/sip/asterisk)
* [FreePBX](/voice/sip/freepbx)
* [FreeSWITCH](/voice/sip/freeswitch)
