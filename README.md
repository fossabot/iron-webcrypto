# iron-webcrypto (beta) [![jsDocs.io](https://img.shields.io/badge/jsDocs.io-reference-blue?style=flat-square)](https://www.jsdocs.io/package/iron-webcrypto) [![npm](https://img.shields.io/npm/dm/iron-webcrypto?style=flat-square)](https://www.npmjs.com/package/iron-webcrypto)
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fbrc-dd%2Firon-webcrypto.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Fbrc-dd%2Firon-webcrypto?ref=badge_shield)

This module is a replacement for [`@hapi/iron`](https://hapi.dev/module/iron/),
written using standard APIs like Web Crypto and Uint8Array, which make this
compatible with a variety of runtimes like Node.js, Deno, Bun, browsers,
workers, and edge environments. Refer `@hapi/iron`'s docs on what it does and
how it works.

> Check out [**unjs/h3**](https://github.com/unjs/h3) and
> [**vvo/iron-session**](https://github.com/vvo/iron-session) to see this module
> in use!

---

## Installation

Simply run:

```sh
npm add iron-webcrypto
```

Change the package manager to whatever you like. On Deno and browsers, you can
use [esm.sh](https://esm.sh/) for importing this:

```ts
import * as Iron from 'https://esm.sh/iron-webcrypto@0.6.0'
```

## Usage

Refer `@hapi/iron`'s docs. There are certain differences.

You need to pass a Web Crypto implementation as the first parameter to each
function. For example:

```ts
Iron.seal(obj, password, Iron.defaults)
```

becomes:

```ts
Iron.seal(_crypto, obj, password, Iron.defaults)
```

where `_crypto` is your Web Crypto implementation. Generally, this will be
available in your context. For example, `globalThis.crypto` in browsers,
workers, edge runtimes, Deno, Bun, and Node.js v19+;
`require('crypto').webcrypto` in Node.js v15+. You can directly use
[`uncrypto`](https://github.com/unjs/uncrypto) for this too. Also, you might
need to polyfill this for older Node.js versions. We recommend using
[`@peculiar/webcrypto`](https://github.com/PeculiarVentures/webcrypto) for that.

There are certain other differences because of the underlying implementation
using standard APIs instead of Node.js-specific ones like `node:crypto` and
`node:buffer`. There might also be differences in certain error messages because
of this.

## Security Considerations

**Users are responsible for implementing `iron-webcrypto` in a secure manner and
ensuring the security of their cryptographic keys. I DO NOT guarantee the
security of this module.** So far, no security vulnerabilities have been
reported, but I am no cryptography expert. Quoting
[MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API):

> The Web Crypto API provides a number of low-level cryptographic primitives.
> It's very easy to misuse them, and the pitfalls involved can be very subtle.
>
> Even assuming you use the basic cryptographic functions correctly, secure key
> management and overall security system design are extremely hard to get right,
> and are generally the domain of specialist security experts.
>
> Errors in security system design and implementation can make the security of
> the system completely ineffective.

As a request, it would be great if someone with expertise in this field could
thoroughly review the code.

## Credits

```txt
@hapi/iron
    Copyright (c) 2012-2022, Project contributors
    Copyright (c) 2012-2020, Sideway Inc
    All rights reserved.
    https://cdn.jsdelivr.net/npm/@hapi/iron@7.0.1/LICENSE.md

@aws-sdk/util-base64
    Copyright 2018-2020 Amazon.com, Inc. or its affiliates. All Rights Reserved.
    https://cdn.jsdelivr.net/npm/@aws-sdk/util-base64@3.208.0/LICENSE
```


[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fbrc-dd%2Firon-webcrypto.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Fbrc-dd%2Firon-webcrypto?ref=badge_large)