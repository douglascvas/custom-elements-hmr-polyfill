# custom-elements-hmr-polyfill

> 100% standard-compliant polyfill to allow WebComponent re-definition at runtime (used for HMR)

[![npm version](https://badge.fury.io/js/custom-elements-hmr-polyfill.svg)](https://badge.fury.io/js/custom-elements-hmr-polyfill)

[![Total alerts](https://img.shields.io/lgtm/alerts/g/vegarringdal/custom-elements-hmr-polyfill.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/vegarringdal/custom-elements-hmr-polyfill/alerts/)

[![Language grade: JavaScript](https://img.shields.io/lgtm/grade/javascript/g/vegarringdal/custom-elements-hmr-polyfill.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/vegarringdal/custom-elements-hmr-polyfill/context:javascript)

[![codecov](https://codecov.io/gh/vegarringdal/custom-elements-hmr-polyfill/branch/master/graph/badge.svg)](https://codecov.io/gh/vegarringdal/custom-elements-hmr-polyfill)

At the time of the creation of this readme, the API `customElements.define(...)` doesn't allow to
re-define a Web Component with the same tag name but a different implementation. This limitation
[made it impossible to do Hot Module Replacement (HMR) with standard Web Components](https://github.com/w3c/webcomponents/issues/829). -
until today.

## Live Demo

-   [Codesandbox](https://codesandbox.io/s/custom-elements-hmr-polyfill-4vd3o)

## How to install it?

-   `npm install custom-elements-hmr-polyfill`

## What does it do?

This polyfill overrides the native browser API `customElement.define` and enables re-definition of
Web Components at runtime.

### Most simple integration

```ts
import { applyPolyfill } from 'custom-elements-hmr-polyfill';

// custom-elements-hmr-polyfill
applyPolyfill();

//  reset the root to trigger rerender after the HMR event
if (document.body) {
    requestAnimationFrame(() => {
        document.body.innerHTML = '';
        document.body.innerHTML = '<root-app></root-app>';
    });
}

export class RootApp extends HTMLElement {
    private name = 'I am RootApp';
    connectedCallback() {
        this.innerHTML = `
      <div style="background-color:green">${this.name}</div>
    `;
    }
}

// PS! customElements.define can be called more then once when running pollyfil
// it need to do this to activate new instance
customElements.define('root-app', RootApp);
```

## Browser Support

This polyfill requires support of the following browser API's (natively).

-   `Proxy`
-   `MutationObserver`
-   `customElements`

## Limitations

None. This polyfill is 100% web standard compliant.

For reference see:
[W3C/WhatWG standard limitation of Web Component re-definition](https://github.com/w3c/webcomponents/issues/829).

## Distribution formats

The bundled npm package contains the following formats:

-   IIFE (`.iife.js`)
-   AMD (`.amd.js`)
-   Common JS (`.cjs.js`)
-   ES Module (`.mjs`)
-   SystemJS (`.system.js`)
-   UMD (`.umd.js`)

You can find single file outputs in `dist/custom-elements-hmr-polyfill.*`, i.e.
`dist/custom-elements-hmr-polyfill.iife.js`.

Furthermore, multiple file outputs are available in `dist/*/**/*.js`. i.e. `dist/AMD/**/*.js`.

-   `AMD`
-   `CommonJS`
-   `ES6`
-   `ES2015`
-   `ESNext`
-   `System`
-   `UMD`

## Advanced: How to start the sample code (of this repo)?

-   `npm run bootstrap`
-   `npm start`

## How to transpile and bundle this polyfill on your own?

-   `npm run bootstrap`
-   `npm build`
