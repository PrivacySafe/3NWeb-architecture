# 3NWeb app manifest

Platform needs information about 3NWeb app, what capabilities are requested, app's name, app's icon, what are entry points for each components, what services are exposed, etc. This information better be presented in typed form like JSON, with strings, numbers, arrays and objects to encapsulated related configuration items. XML is too complex. JSON types can be put into JSON file and YAML file, and we can have TyepScript type descriptions. Thus, we choose JSON.

Docs are work in progress, but they are written after at least one implementation exists, allowing to quickly link to it, and it least to give a gist of technical nuances. For manifest, see [TypeScript interface AppManifest here](https://github.com/3nsoft/core-platform-electron/blob/74280fef796e295f9e67b64bd92a82e6abdde8d4/ts-code/app-init/app-settings.ts#L35)
