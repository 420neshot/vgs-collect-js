<p align="center">
  <a href="https://www.verygoodsecurity.com/" rel="nofollow">
    <img src="https://avatars0.githubusercontent.com/u/17788525" width="128" alt="VGS Logo">
  </a>
  <h3 align="center">VGS Collect.js</h3>

  <p align="center">
    Script loading module for VGS Collect.js
    <br />
    <a href="https://www.verygoodsecurity.com/docs/vgs-collect/js/overview"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/verygoodsecurity/vgs-collect-js/issues">Report Bug</a>
    ·
    <a href="https://github.com/verygoodsecurity/vgs-collect-js/issues">Request Feature</a>
  </p>
</p>

* [Overview](#overview)
* [Installation](#installation)
* [How to use](#how-to-use)
* [Documentation](#documentation)
* [Contributing](#contributing)
* [Built With](#built-with)
* [Contact](#contact)

## Overview

[VGS Collect.js](https://www.verygoodsecurity.com/docs/vgs-collect/js/overview) is a JavaScript library that allows you to securely collect data via any form. Instantly create custom forms that adhere to PCI, HIPAA, GDPR, or CCPA security requirements. [VGS](https://www.verygoodsecurity.com/) intercepts sensitive data before it hits your servers and replaces it with aliased versions while securing the original data in our vault. The form fields behave like traditional forms while preventing access to the unsecured data by injecting secure iframe components.

This module intended to simplify [VGS Collect.js](https://www.verygoodsecurity.com/docs/vgs-collect/js/overview) script loading process. You can still use the conventional way and just stick a reference to the script in the HEAD section of your page but you may lose some beneficial advantages the package provides:

- Error handling
- Fallback CDN managing
- Reduced latency of cross-origin requests

## Installation

Install the package using `npm`:

```
npm install @vgs/collect-js
```

## How to use

The imported function inserts the `<script>` tag to the document head or body and returns the `VGSCollect` instance as the result of resolved Promise. The script won't be loaded until `loadVGSCollect()` invoked. In order to speed up cross-domain loading, `dns-prefetch` and `preconnect` were added as a side effect.

```javascript 
import { loadVGSCollect } from '@vgs/collect-js';

// load script
const VGSCollectInstance = await loadVGSCollect({
  vaultId: '<vault_id>', // required
  environment: 'sandbox',
  version: '2.0'
}).catch((e) => {
  // script was not loaded
});

// https://www.verygoodsecurity.com/docs/vgs-collect/js/integration#form-state
const VGSCollectForm = VGSCollectInstance.init(state => { console.log(state); });

// https://www.verygoodsecurity.com/docs/vgs-collect/js/integration#create-and-setup-form-fields
VGSCollectForm.field({...});
VGSCollectForm.field({...});
VGSCollectForm.field({...});

// https://www.verygoodsecurity.com/docs/vgs-collect/js/integration#setup-form-submission
VGSCollectForm.submit(...);
```

### loadVGSCollect(config)

Available properties:

| Property    | Type   | Description                                                                                                                                                                           | Default     |
|-------------|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| vaultId     | string | Every vault has a unique vault id - it’s a string value beginning with the prefix tnt                                                                                                 | required    |
| environment | string | Vault environment. Can be `sandbox`, `live`, or one with a specified data region (e.g `live-eu-1`).                                                                                   | `'sandbox'` |
| version     | string | You can specify library version being loaded. Version must be >= 2.0. Please check our [Changelog](https://www.verygoodsecurity.com/docs/vgs-collect/js/changelog) for more details.  | `'2.0'`     |

### .init(callback)

A wrapper over original [`.create()`](https://www.verygoodsecurity.com/docs/vgs-collect/js/integration#form-initialization) method. As we have already received `vault_id` and `environment` from the `loadVGSCollect()` argument, there is no need to specify those params again. The method only returns the form state in the callback. You can still use `.create()` if necessary.

```javascript
VGSCollect.init(state => { console.log(state); });
```

## Documentation

Full abilities of VGS Collect.js and integration details you can find in our [documentation](https://www.verygoodsecurity.com/docs/vgs-collect/js/integration).

## Contributing 

1. Fork the project
2. Create your feature branch (`git checkout -b feaure/my-amazing-feature`)
3. Commit your changes (`git commit -m 'feature: added amazing feature'`)
4. Push to the branch (`git push origin feature/my-amazing-feature`)
5. Open a Pull Request

## Built with

* [Typescript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)
* [tsdx template](https://github.com/formium/tsdx)

## Contact

If you have any questions please reach out to [support](mailto:support@verygoodsecurity.com) or open issue [here](https://github.com/verygoodsecurity/vgs-collect-js/issues).