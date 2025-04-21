# 📃 3NWeb App Manifest

The 3NWeb app manifest provides essential information about the app, including its requested capabilities, name, icon, entry points for each component, and the services it exposes for example via API. This data is best represented in a typed format, such as JSON, which allows us to clearly define configuration items using strings, numbers, arrays, and objects.

XML is avoided due to its complexity. Instead, JSON files, along with corresponding YAML files, are used to encapsulate configuration data, ensuring clarity and simplicity. TypeScript type definitions are also provided to maintain consistency and accuracy across the system.

By using this structured approach, the 3NWeb platform can better manage app configurations, permissions, and services, enabling developers to integrate apps seamlessly. 

For the manifest details, refer to the [TypeScript interface AppManifest](https://github.com/3nsoft/core-platform-electron/blob/74280fef796e295f9e67b64bd92a82e6abdde8d4/ts-code/app-init/app-settings.ts#L35). This manifest file defines the app's name, version, domain, and the capabilities it requests, such as storage access or communication services. This structure helps users and developers understand exactly what an app can do and what permissions it requires.

---
The documentation is a work in progress. For active deployment details, refer to the [PrivacySafe](https://github.com/PrivacySafe) implementation.
