# Component Danx

[![npm](https://img.shields.io/npm/v/quasar-ui-danx.svg?label=quasar-ui-danx)](https://www.npmjs.com/package/quasar-ui-danx)
[![npm](https://img.shields.io/npm/dt/quasar-ui-danx.svg)](https://www.npmjs.com/package/quasar-ui-danx)

**Compatible with Quasar UI v2 and Vue 3**.


# Component Danx
> Short description of the component




# Usage

## Quasar CLI project


Install the [App Extension](../app-extension).

**OR**:


Create and register a boot file:

```js
import Vue from 'vue'
import Plugin from 'quasar-ui-danx'
import 'quasar-ui-danx/dist/index.css'

Vue.use(Plugin)
```

**OR**:

```html
<style src="quasar-ui-danx/dist/index.css"></style>

<script>
import { Component as Danx } from 'quasar-ui-danx'

export default {
  
  components: {
    Danx
  }
  
  
}
</script>
```

## Vue CLI project

```js
import Vue from 'vue'
import Plugin from 'quasar-ui-danx'
import 'quasar-ui-danx/dist/index.css'

Vue.use(Plugin)
```

**OR**:

```html
<style src="quasar-ui-danx/dist/index.css"></style>

<script>
import { Component as Danx } from 'quasar-ui-danx'

export default {
  
  components: {
    Danx
  }
  
  
}
</script>
```

## UMD variant

Exports `window.danx`.

Add the following tag(s) after the Quasar ones:

```html
<head>
  <!-- AFTER the Quasar stylesheet tags: -->
  <link href="https://cdn.jsdelivr.net/npm/quasar-ui-danx/dist/index.min.css" rel="stylesheet" type="text/css">
</head>
<body>
  <!-- at end of body, AFTER Quasar script(s): -->
  <script src="https://cdn.jsdelivr.net/npm/quasar-ui-danx/dist/index.umd.min.js"></script>
</body>
```
If you need the RTL variant of the CSS, then go for the following (instead of the above stylesheet link):
```html
<link href="https://cdn.jsdelivr.net/npm/quasar-ui-danx/dist/index.rtl.min.css" rel="stylesheet" type="text/css">
```

# Setup
```bash
$ yarn
```

# Developing
```bash
# start dev in SPA mode
$ yarn dev

# start dev in UMD mode
$ yarn dev:umd

# start dev in SSR mode
$ yarn dev:ssr

# start dev in Cordova iOS mode
$ yarn dev:ios

# start dev in Cordova Android mode
$ yarn dev:android

# start dev in Electron mode
$ yarn dev:electron
```

# Building package
```bash
$ yarn build
```

# Adding Testing Components
in the `ui/dev/src/pages` you can add Vue files to test your component/directive. When using `yarn dev` to build the UI, any pages in that location will automatically be picked up by dynamic routing and added to the test page.

# Adding Assets
If you have a component that has assets, like language or icon-sets, you will need to provide these for UMD. In the `ui/build/script.javascript.js` file, you will find a couple of commented out commands that call `addAssets`. Uncomment what you need and add your assets to have them be built and put into the `ui/dist` folder.

# Donate
If you appreciate the work that went into this, please consider [donating to Quasar](https://donate.quasar.dev).

# License
MIT (c) Dan <dan@flytedesk.com>
