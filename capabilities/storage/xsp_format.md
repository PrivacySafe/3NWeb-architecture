# 🔢 XSP Format for Encrypted Files

Each [NaCl](https://nacl.cr.yp.to/index.html) cipher must be read completely before any plaintext is output. This requirement makes reading large files awkward. Therefore, we need a file format that satisfies the following requirements:

* The file should be split into segments.
* It should be possible to randomly read segments.
* Each segment should include a Poly cipher and allow for integrity checks.
* It should be possible to randomly add or remove segments without re-encrypting the entire file.
* Segments' nonces should never be reused, even when performing partial changes to the file, without completely re-encrypting the file.
* It should be possible to detect if segments are reshuffled.
* There should be cryptographic proof of the complete file size for files with a known size.
* There should be a stream-like setting where segments can be encrypted and read without knowing the final length in advance.
* Once the complete length of the stream is known, switching to a known-length setting should be inexpensive.

We call this format **XSP**, which stands for **XSalsa+Poly**, to indicate that the file layout is specifically designed for storing NaCl's secret box ciphers. An XSP file consists of a header and zero or more segments with data.

Segments are NaCl's packages of Poly and XSalsa ciphers:
```
    +------+ +---------------+
    | poly | |  data cipher  |
    +------+ +---------------+
    | <--  NaCl format   --> |
```
The header is packed with its nonce into the WN format (introduced in ecma-nacl):
```
    +-------+ +------+ +---------------+
    | nonce | | poly | |  data cipher  |
    +-------+ +------+ +---------------+
    | <----       WN format      ----> |
```

## Header Data

The header provides information about the segments, their nonces, and expected sizes. It contains the following:
```
    |<- 1 byte ->| |<-   2  ->| |<-  n*31  ->|
    +------------+ +----------+ +------------+
    |   version  | | seg size | | seg chains |
    +------------+ +----------+ +------------+
```
* The version byte is a positive integer. The layout described in this section corresponds to versions 1 and 2.
* Two big-endian bytes represent a non-negative integer for the segment content size in 256-byte units. The packed segment size is this value plus 16 bytes (for Poly). The last segments in segment chains may be shorter.
* Information about `n=0,1,...` segment chains.

Data segments come in chains. Segments within the same chain have consecutive nonces. All segments should be the same size, except for the last segment in a chain.

The segment chain is described in the header with the following bytes:
```
    |<-   4 bytes  ->| |<-  3 bytes  ->| |<-     24 bytes    ->|
    +----------------+ +---------------+ +---------------------+
    | number of segs | | last seg size | | first segment nonce |
    +----------------+ +---------------+ +---------------------+
    |<-                    seg chain                         ->|
```
* The first 4 bytes are a big-endian encoded non-negative integer representing the number of segments in this chain.
* The following 3 bytes are a big-endian encoded non-negative integer representing the last segment's content length in this chain.
* The final 24 bytes are the nonce of the first segment in the chain. Nonces for all other segments are calculated by incrementing this nonce. For example, incrementing this nonce by one gives the nonce for the second segment in the chain, and so on. The nonce increment function comes from ecma-nacl, treating the 24-byte nonce as three 64-bit unsigned integers, to which the respective number is added.

If the writer needs to send the file's header before knowing the total file length, the last chain can be infinite. The number of segments in the infinite chain is set to `0xffffffff`, which represents the maximum possible segment index. The last segment's size in the infinite chain is set to the common segment size.

Note that since the nonce for each chain is unique, it is possible to calculate the differences between two versions, i.e., identify which segments of the file have changed and which have remained the same. Segments that stay the same guarantee that the corresponding sections of the file's content remain unchanged.

## Current Format Versions

Currently, we identify two versions of content:
* Version 1 indicates [continuous load](https://github.com/PrivacySafe/core-3nweb-client-lib/blob/master/ts-code/lib-client/3nstorage/xsp-fs/xsp-payload-v1.ts);
* Version 2 indicates [segmented load](https://github.com/PrivacySafe/core-3nweb-client-lib/blob/master/ts-code/lib-client/3nstorage/xsp-fs/xsp-payload-v2.ts). Indirect packing allows attributes to be held, written out of order, and leaves space for increasing or obfuscating the size.

## Object Versions

Each object may go through multiple versions, and it is useful to have both the object ID and version imprinted into the package. 

Imagine a client needs to retrieve a specific object and version from a server. If the server provides an incorrect version, it should be immediately noticeable. XSP handles this as follows.

The header is a package with a nonce. The nonce is the initial (zeroth) nonce for an object, incremented by the version number. The zeroth nonce can serve as the object ID. If you expect a particular ID+version combination, you expect to use a particular nonce to open the header.

In a scenario where two clients try to write the same new version of an object concurrently, they may send headers that use the same nonce. This creates a potential for crypt-analysis of the header. However, since the header only contains information about the segment structure and segment nonces, such crypt-analysis does not compromise the content. When creating a new version, both clients will generate new random nonces for use in the segment chains that form either the entire file or the diff of the new version, ensuring no nonce reuse.

---
The documentation is a work in progress. For active deployment details, refer to the [PrivacySafe](https://github.com/PrivacySafe) implementation.
