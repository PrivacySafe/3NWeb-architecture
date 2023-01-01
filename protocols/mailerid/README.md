# MailerId protocol

MailerId process involves three parties:
 1. Identity provider (identity service)
 2. User of an identity service
 3. Relying party, to who user wants to prove her identity

![Provisioning phase](./flow_in_provisioning_stage_of_mailerid.png)

In the first stage, provisioning stage, User generates a signing key pair, logs into the service, and asks Identity Provider to make (provision) a certificate for his public key.

User's certificate can be used till its expiration. Therefore, provisioning step does not need to be repeated for a while (usually a few hours).

User's login in MailerId is done via [Public Key Login (PKL) process](../pkl/README.md). PKL does not require having a browser, removing BrowserID's vulnerable part.

With a provisioned certificate for his signing key, user can sign his other public key. For example, ASMail introductory key should be signed with MailerId key.

![MailerId used to sign other key and passed to peer, who checks all signatures](./flow_in_usage_of_mailerid_1.png)

When Alice (relying party) has to verify a key that is claimed to be for `Bob@montague.it`, the following steps are taken:
 1. DNS record for `montague.it` is checked for a location of MailerId providing service.
 2. Provider's root certificate is retrieved from service location with a request that is the same for all relying parties. Such request does not contain neither information about the user, nor about relying party, in a spirit of POLA.
 3. Alice checks complete certificate chain of signatures/certificates.

There is a MailerId login sequence similar to that in BrowseId.

![MailerId used to sign assertion within MailerId login sequence](./flow_in_usage_of_mailerid_2.png)

Docs are work in progress. For now we can point to [docs-like definitions](https://github.com/3nsoft/spec-server/tree/master/ts-code/lib-common/service-api/mailer-id).

Together with protocol definition we will also specify actual tests, [like these ones](https://github.com/3nsoft/spec-server/blob/master/ts-code/tests/protocols/mailerid.ts), giving a tool to check implementations of MailerId service.
