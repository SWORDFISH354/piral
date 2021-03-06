[![Piral Logo](https://github.com/smapiot/piral/raw/master/docs/assets/logo.png)](https://piral.io)

# [Piral NgJS](https://piral.io) &middot; [![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/smapiot/piral/blob/master/LICENSE) [![npm version](https://img.shields.io/npm/v/piral-ngjs.svg?style=flat)](https://www.npmjs.com/package/piral-ngjs) [![tested with jest](https://img.shields.io/badge/tested_with-jest-99424f.svg)](https://jestjs.io) [![Gitter Chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/piral-io/community)

This is a plugin that only has a peer dependency to `piral-core`. What `piral-ngjs` brings to the table is a set of Pilet API extensions that can be used with `piral` or `piral-core`.

The set includes an Angular.js converter for any component registration, as well as a `fromNgjs` shortcut and a `NgjsExtension` component.

By default, these API extensions are not integrated in `piral`, so you'd need to add them to your Piral instance.

## Documentation

The following functions are brought to the Pilet API.

### `fromNgjs()`

Transforms a standard Angular.js module with a named component into a component that can be used in Piral, essentially wrapping it with a reference to the corresponding converter.

### `NgjsExtension`

The extension slot module to be referenced in Angular.js module definitions. Allows using an Angular.js custom element named `extension-component`.

## Usage

> For authors of pilets

You can use the `fromNgjs` function from the Pilet API to convert your Angular.js modules to components usable by your Piral instance.

Example use:

```ts
import { PiletApi } from '<name-of-piral-instance>';
import { createAngularJsPage } from './AngularJsPage';

export function setup(piral: PiletApi) {
  const AngularJsPage = createAngularJsPage(piral.NgjsExtension.name);
  piral.registerPage('/sample', piral.fromNgjs(AngularJsPage));
}
```

Within Angular.js components the Piral Angular.js extension component can be used by referring to `NgjsExtension`, e.g.,

```html
<extension-component name="name-of-extension"></extension-component>
```

## Setup and Bootstrapping

> For Piral instance developers

The provided library only brings API extensions for pilets to a Piral instance. The Piral instance still needs to be configured properly to support Angular.js 1.x.

For the setup itself you'll need to import `createNgjsApi` from the `piral-ngjs` package.

```ts
import { createNgjsApi } from 'piral-ngjs';
```

The integration looks like:

```ts
const instance = createInstance({
  // important part
  extendApi: [createNgjsApi()],
  // ...
});
```

## License

Piral is released using the MIT license. For more information see the [license file](./LICENSE).
