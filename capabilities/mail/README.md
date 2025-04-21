# 💬 Messaging Capability

The [ASMail protocol](../../protocols/asmail/README.md), used for communication within the client platform, ensures that all messages are transmitted as encrypted blobs. The encryption and key management are handled by the clients themselves.

![Keys rotation](mail_keys_rotation.png)

Each message is encrypted with a unique key, and that key is further encrypted using public key cryptography. To enhance security, the public keys of peers are rotated regularly. This reduces the risk of key leakage in case of breaches.

When using randomly generated keys, each key is unique, so the recipient can easily determine the sender. If the key isn't provided, the recipient must try all possible keys to find the correct one. To make this process more efficient, the protocol allows passing a key pair label that helps clients find the correct key faster.

![Plaintext metadata of message](metadata_message_part.png)

[This implementation](https://github.com/PrivacySafe/core-3nweb-client-lib/tree/master/ts-code/core/asmail) uses random pair IDs to minimize the number of decryption attempts, without turning the pair ID into a pseudonymous identifier for the sender.

Each message consists of one or more encrypted blobs, with the main object containing an encrypted JSON defined by the [MsgStruct definition](https://github.com/PrivacySafe/core-3nweb-client-lib/blob/master/ts-code/api-defs/asmail.d.ts#L208). Attachments, which are standard files or folders in the 3NStorage file system, are included as encrypted objects within the message.

The platform standardizes messages exchanged between the app and platform using [protobuf formats](https://github.com/PrivacySafe/core-3nweb-client-lib/blob/master/protos/asmail.proto). Additionally, specific language bindings, such as [TypeScript definitions](https://github.com/PrivacySafe/core-3nweb-client-lib/blob/master/ts-code/api-defs/asmail.d.ts), are also part of the standard.

We also provide [tests](https://github.com/PrivacySafe/core-3nweb-client-lib/blob/master/ts-code/tests/apis/asmail.ts) to ensure the platform implementation meets the messaging standards, offering a way to verify app-to-platform integration.

---
The documentation is a work in progress. For active deployment details, refer to the [PrivacySafe](https://github.com/PrivacySafe) implementation.
