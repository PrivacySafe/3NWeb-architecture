For the full version of this document, please read the repository [Architecture Overview](../README.md). We include the sections that concern federation below, as the 3NWeb approach is unique while learning much from other existing approaches.

## 🔏 Least Authority in the Client-Server Model

Client-server models dominate the internet, but they often violate privacy principles. By applying the **Principle of Least Authority (POLA)**, we can reframe these designs to minimize abuse and data leakage.

> The **3N Principle** applied here:
>
> 1. **No plain-text content** is sent to servers  
> 2. **No unnecessary metadata** is included in client-server exchanges  
> 3. **Nothing on the server** can be exploited if (1) and (2) are respected

While a few efforts like [PGP/GPG](https://www.ietf.org/archive/id/draft-koch-openpgp-2015-rfc4880bis-02.html) have succeeded in giving users true data control, they remain the exception. The dominant technologies favor centralized systems where user data is aggregated. This often introduces security and privacy risks. We seek to make user-respecting design the **default**. By lowering the barrier to develop secure, private apps and making it more economical to run them, we shift the baseline toward ethical digital systems.

Apps built using our stack aim to replace centralized “cloud” tools while preserving user freedom, metadata minimization, and offline access.

## 🌐 Federation: Classical vs. Web-Based

### 🔁 Classical Federation

Popular in systems like [Jabber/XMPP](https://xmpp.org/rfcs/) or [Matrix](https://spec.matrix.org), this model relies on inter-server cooperation. Each user connects to their “home” server, which then talks to peers’ servers.

![Roles in Classical Federation](roles_in_classical_federation.png)

Users have accounts at servers. A user owns some resource on their home server and connects only to it, while servers relay messages on their behalf.

![Information flows in Classical Federation](data_flows_in_classical_federation.png)

**Problems:**
- Requires trust in cooperating vendors
- Leaks metadata due to server-level routing
- Can break if large players refuse to interoperate

![Problems in Classical Federation](two_problems_in_classical_federation.png)

#### 🕸️ Web-Style Federation

In contrast, the web model treats each domain or server as autonomous. There is **no expectation of cooperation** between servers. Apps communicate **peer-to-peer**, only as needed.

**Benefits:**
- Minimal metadata
- Easier to preserve privacy
- No dependency on large vendor coordination

![Data Flows in Web Federation](data_flows_in_web_federation.png)

## 🛠️ Implementation & Standards

The protocols here form the foundation for secure, app-centric systems. Real-world applications like those in the [PrivacySafe Suite](https://privacysafe.app) demonstrate these designs in action.

### 💻 On the Client

Apps rely on a platform layer that provides secure services: file access, networking, cryptography, and more. Capabilities are granted based on app manifests — a clear, auditable permission system.

![Client Platform Diagram](../implementation/implementation_parts.png)

Each capability corresponds to a standard service:

- 📩 **Messaging** → [ASMail protocol](../protocols/asmail/README.md)
- 📂 **Storage** → [3NStorage protocol](../protocols/3nstorage/README.md)
- 🔑 **Identity** → [MailerId protocol](../protocols/mailerid/README.md)

Additional utilities connect apps to the OS or other services securely.

Apps use a [manifest file](../app-manifest/README.md)) to declare required capabilities. These capabilities may also include services that help compose multiple apps into a coherent system on user devices.

![Capabilities and Protocols](../implementation/caps_and_protocols.png)

---
The documentation is a work in progress. For active deployment details, refer to the [PrivacySafe](https://github.com/PrivacySafe) implementation.
