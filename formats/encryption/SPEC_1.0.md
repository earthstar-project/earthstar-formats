# About format

<dl>
	<dt>Namespace</dt><dd>`encryption`</dd>
	<dt>Version</dt><dd>1.0</dd>
</dl>

TODO: Namespace name is a bit odd - ideas on better one?

This is an application format for describing how to decrypt other elements of the same share.

It's intended that this be handled automatically by the Earthstar libraries, so applications don't need to thing about the details here.

i.e.
- App starts by writing out some keys under /encryption
- Then any keys written after are transparently encrypted (both path and/or payload) before being stored
- And likewise any list/get of the keyspace happens after decryption

This also lends itself to different users of the same application format having different setups for encryption, and other clients reading it will apply the correct settings.

## Motivation

Trying to predict everything about how different users will want to use encryption of paths and payloads is challenging, to say the least.

Decoupling this and allowing this to vary across different clients is helpful.

This also allows for a lot of the detail to be done by the standard library, instead of needing to be coded by individual clients.

### Path Encryption settings

The path format of a path settings document is:

```
/encryption/1.0/{PATH}/path.yaml
```

### fields

```
recursive: true # Whether or not this applies only to one level, or all the way down the tree
```

TODO

### Payload Encryption settings

The path format of a payload settings document is:

```
/encryption/1.0/{PATH}/payload.yaml
```

### fields

```
recursive: true # Whether or not this applies only to one level, or all the way down the tree
```

TODO
