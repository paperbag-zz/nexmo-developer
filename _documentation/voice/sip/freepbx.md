---
title: FreePBX
description: How to setup Nexmo SIP with FreePBX
---

# FreePBX

Below we provide example configurations for using Nexmo's SIP service with [FreePBX](http://www.freepbx.org).

## Inbound configuration

````
host=173.193.199.24
type=friend
insecure=port,invite
;Add your codec list here.
; Note: Use "ulaw" for US only, "alaw" for the rest of the world.
allow=ulaw,alaw,g729
dtmfmode=rfc2833

host=174.37.245.34
type=friend
insecure=port,invite
;Add your codec list here.
; Note: Use "ulaw" for US only, "alaw" for the rest of the world.
allow=ulaw,alaw,g729
dtmfmode=rfc2833

host=5.10.112.121
type=friend
insecure=port,invite
;Add your codec list here.
; Note: Use "ulaw" for US only, "alaw" for the rest of the world.
allow=ulaw,alaw,g729
dtmfmode=rfc2833

host=5.10.112.122
type=friend
insecure=port,invite
;Add your codec list here.
; Note: Use "ulaw" for US only, "alaw" for the rest of the world.
allow=ulaw,alaw,g729
dtmfmode=rfc2833

host=119.81.44.6
type=friend
insecure=port,invite
;Add your codec list here.
; Note: Use "ulaw" for US only, "alaw" for the rest of the world.
allow=ulaw,alaw,g729
dtmfmode=rfc2833

host=119.81.44.7
type=friend
insecure=port,invite
;Add your codec list here.
; Note: Use "ulaw" for US only, "alaw" for the rest of the world.
allow=ulaw,alaw,g729
dtmfmode=rfc2833
````

## Outbound configuration

````
host=sip.nexmo.com
  type=friend
  insecure=port,invite
  qualify=yes
  ;Add your codec list here.
  ;Note: Use "ulaw" for US only, "alaw" for the rest of the world.
  allow=ulaw,alaw,g729
  dtmfmode=rfc2833

  username=<key>
  fromuser=<long_virtual_number>
  secret=<secret>

  Register String
  <key>:<secret>@sip.nexmo.com
````
