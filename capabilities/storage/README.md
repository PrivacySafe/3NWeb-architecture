# Storage capability

Most apps/programs need storage and file system is the simplest storage expected by app developers. On the other hand storage uploaded to servers shouldn't have any content and metadata visible.

Storage saves blobs/objects labeled by randomly generated ids (object ids). Content of blobs is cipher in [XSP format](./xsp_format.md) that helps with changes, checks, versioning, etc. XSP format is articulated for usages with high level and simple api of [NaCl](http://nacl.cr.yp.to/) crypto library, like. Stylistic of XSP can be used for library with NaCl's stylistic of api surface, when/if client wants it. And alternatives can be added as optional sections in 3NWeb's overall heap of standards/formats/protocols.

Currently there are two versions of content that is encrypted in XSP objects. [Version 1](https://github.com/3nsoft/core-3nweb-client-lib/blob/master/ts-code/lib-client/3nstorage/xsp-fs/xsp-payload-v1.ts) are just bytes without any file system info. [Version 2](https://github.com/3nsoft/core-3nweb-client-lib/blob/master/ts-code/lib-client/3nstorage/xsp-fs/xsp-payload-v2.ts) uses sections that allow to have randomly placed writes on app's side while XSP encrypted segements come out as if appends happen. Appending writes simplify what should be synchronized to the server. From an infosec perspective, this also obfuscates file write pattern observable by servers.

[Implementation](https://github.com/3nsoft/core-3nweb-client-lib/tree/master/ts-code/lib-client/3nstorage/xsp-fs) contains details of how file system entities are layed down in bytes. We'll move this implicit info into explicit format standard. For now, the most important points to note is that every object is encrypted by its own randomly generated key, that is stored in parent folder.

![Cascade of encryption keys](./keys_cascade.png)

Such cascade of encryption keys allows sharing of file system sub-tree without exposing keys to other places.

App developers don't always need to synchronize data between instances on different devices. Sometimes only local storage is needed. Simplest route to accomodate this is to have same encryption and packing for both local and synced storages. Local storage simply doesn't have syncing functionality, while all persistent data to disks is encrypted and leaks not metadata ([see code](https://github.com/3nsoft/core-3nweb-client-lib/tree/master/ts-code/core/storage)).

App-facing platform side standardizes on protobuf forms of messages: [storage](https://github.com/3nsoft/core-3nweb-client-lib/blob/master/protos/storage.proto), [file](https://github.com/3nsoft/core-3nweb-client-lib/blob/master/protos/file.proto), [fs](https://github.com/3nsoft/core-3nweb-client-lib/blob/master/protos/fs.proto). Additionally, 3NWeb standards may also include language specific forms, like [this TypeScript definitions](https://github.com/3nsoft/core-3nweb-client-lib/blob/master/ts-code/api-defs/files.d.ts).

For communication with 3NStorage servers platform uses [3NStorage protocol](../../protocols/3nstorage/README.md).

*Docs are work in progress, but links to code point to working implementation, to least give a gist of technical nuances.*
