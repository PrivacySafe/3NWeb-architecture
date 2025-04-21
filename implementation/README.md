For the full version of this document, please read the repository [Architecture Overview](../README.md). We include the sections that concern implementation below.

## 🛠️ Implementation & Standards

The protocols here form the foundation for secure, app-centric systems. Real-world applications like those in the [PrivacySafe Suite](https://privacysafe.app) demonstrate these designs in action.

### 💻 On the Client

Apps rely on a platform layer that provides secure services: file access, networking, cryptography, and more. Capabilities are granted based on app manifests — a clear, auditable permission system.

![Client Platform Diagram](implementation_parts.png)

Each capability corresponds to a standard service:

- 📩 **Messaging** → [ASMail protocol](../protocols/asmail/README.md)
- 📂 **Storage** → [3NStorage protocol](../protocols/3nstorage/README.md)
- 🔑 **Identity** → [MailerId protocol](../protocols/mailerid/README.md)

Additional utilities connect apps to the OS or other services securely.

Apps use a [manifest file](../app-manifest/README.md)) to declare required capabilities. These capabilities may also include services that help compose multiple apps into a coherent system on user devices.

![Capabilities and Protocols](caps_and_protocols.png)

- 🎨 **App Composition Tools**:
  - `appRPC`: Connects to components within the same app.
  - `otherAppsRPC`: Connects to services provided by other apps.
  - `exposeService`: Publishes services for other apps to use. For instance, when porting a traditional web app to 3NWeb, backend functions like cloud lambdas are refactored as services exposed here via RPC.

- 🔢 **Runtime Utilities**:
  - `connectivity`: Detects if the client is offline.
  - `closeSelf`: Allows an app to terminate its own process.
  - `log`: Sends errors and warnings to the platform log.

- 📁 **OS Integration Utilities**:
  - `shell.fileDialog`: Opens native file selection dialogs.
  - `shell.mountFS`: Mounts a 3NWeb storage folder for access by traditional (non-3NWeb) programs.
  - `shell.userNotifications`: Sends native notifications through the device OS UI.

- ⚙️ **Platform Services**:
  - `logout`: Logs out the user, shuts down core processes, and clears memory-resident keys.
  - `apps.opener`: Opens 3NWeb apps when triggered by the user.
  - `apps.downloader`: Finds and downloads new 3NWeb apps, or updates existing ones.
  - `apps.installer`: Installs new apps into the user’s platform.
  - `platform`: Checks for updates to the platform software itself.

### 👤 User IDs & Identity

Each user is globally identifiable via a `<username>@domain` format, similar to email or instant messaging protocols. Identity resolution follows canonical rules: no whitespace, case-insensitive.

Example:  
`Bob Marley @3nweb.com` becomes `bobmarley@3nweb.com`

### 🔎 Service Discovery

Services are discovered via DNS `TXT` records or `.well-known` endpoints on [Tor](https://spec.torproject.org). This approach decouples domain ownership from server location, enabling flexible deployment and decentralization.

Example DNS entries:

```
asmail=3nweb.net/asmail
mailerid=mailerid.org
3nstorage=3nweb.net/3nstorage
```

---
The documentation is a work in progress. For active deployment details, refer to the [PrivacySafe](https://github.com/PrivacySafe) implementation.
