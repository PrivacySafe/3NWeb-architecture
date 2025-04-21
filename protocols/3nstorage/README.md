# 📁 3NStorage protocol

![Information flow in 3NStorage](data_flow_in_3nstorage.png)

Please refer to our [Typescript definitions](https://github.com/PrivacySafe/spec-server/tree/master/ts-code/lib-common/service-api/3nstorage). 

App-facing platforms standardize communication with protobuf messages for [storage](https://github.com/PrivacySafe/core-3nweb-client-lib/blob/master/protos/storage.proto), [files](https://github.com/PrivacySafe/core-3nweb-client-lib/blob/master/protos/file.proto), and [file systems](https://github.com/PrivacySafe/core-3nweb-client-lib/blob/master/protos/fs.proto). 3NWeb also offers language-specific implementations, such as [TypeScript definitions](https://github.com/PrivacySafe/core-3nweb-client-lib/blob/master/ts-code/api-defs/files.d.ts).

We provide tests, like [these](https://github.com/PrivacySafe/core-3nweb-client-lib/blob/master/ts-code/tests/apis/storage.ts), [these](https://github.com/PrivacySafe/core-3nweb-client-lib/tree/master/ts-code/tests/apis/fs-checks), and [these](https://github.com/PrivacySafe/core-3nweb-client-lib/tree/master/ts-code/tests/apis/file-sink-checks) to ensure compliance with the platform’s standards.

---
The documentation is a work in progress. For active deployment details, refer to the [PrivacySafe](https://github.com/PrivacySafe) implementation.
