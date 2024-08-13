---
eleventyComputed:
  title: Unmanaged Providers (Password Reset Only)
  description: 
  order: 30
---

Within {{ en.DVPAM }}, a ***provider*** *typically* performs the entire password management lifecycle from ***discovery***, ***heartbeat*** and ***password rotation***. However, sometimes it’s not always appropriate, necessary or possible to maintain the entire lifecycle for an ***identity provider***; this is where ***unmanaged providers*** or sometimes referred to as ***password reset only providers*** come in.

***Unmanaged providers*** perform only a single phase of the password management lifecycle; the ***password rotation*** phase. Unlike other ***providers***, they are only capable of resetting a password for an ***account*** on an ***identity provider***.

![Unmanaged providers](https://cdnweb.devolutions.net/docs/docs_en_server_ServerOp2108.png)
