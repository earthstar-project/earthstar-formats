# About format

<dl>
	<dt>Namespace</dt><dd>`did`</dd>
	<dt>Version</dt><dd>1.0</dd>
</dl>

This is an application format for describing how information relating to a particular [Decentralized Identifiers (DID)](https://www.w3.org/TR/did-core/) is stored in an Earthstar share.

## Document prefix

The path format prefix (after any path decryption is performed) is:
```
/did/1.0/{DID}/...
```

e.g. `/did/1.0/did:key:z6MkhaXgBZDvotDkL5257faiztiGiC2QtKLGpbnnEGta2doK/...`

Note this is a prefix - it's expected you'd use another application format under this structure to actually define the keys.

## Document paths

The document `/did/1.0/{DID}/did.json` may contain the [standard JSON representation](https://www.w3.org/TR/did-core/#json) of the DID Document.

If it exists, and the DID is of the `did:key` form and matches the subspace, and the namespace is a communal namespace, then this is to be treated as the canonical DID Document for that ID

TODO: Is this needed? Need to consider the use-cases here more.

## Why DIDs?

There are many reasons why people might need to rotate cryptographic identifiers (compromise, loss, privacy).

So, providing options that support this is important.

The existence of [did:key](https://w3c-ccg.github.io/did-method-key/) means that if you just want to use your subspace ID, you can.

But other users might use [did:web](https://w3c-ccg.github.io/did-method-web/) or other choices.

This also allows for use of newer / better / different forms of ID, without changing the underlying protocol.

## Resolution / Verification

Information found under a did prefix MUST NOT be trusted to belong to that did, without first [resolving](https://w3c-ccg.github.io/did-resolution/#resolving) the did (using the standard protocol for that did method) into a DID Document, and that DID Document must contain an `alsoKnownAs` entry matching the current subspace, in did:key form. (Naturally, a did:key:<subspace> that matches the subspace it's in is always valid).

Or, should this be an alsoKnownAs with an `earthstar://` specific type thing?

Or, is the authentication verification relationship appropriate?

Not sure on which of the above three is most semantically correct - but there definitely needs to be something that says "Yes, this earthstar subspace is allowed to be me"

Other implementations: atproto uses `alsoKnownAs` with an entry of the form `at://`
