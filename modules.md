# Modules

TypeScript is made to adapt to JavaScript. And JavaScript itself has had many module systems for different environments and times. Most notably:

* The browser console "vanilla" environment is module-less. Every imported file lives in the global scope;
* node.js traditionally uses the "commonjs" module syntax;
* Modern front-end code built with module bundlers usually use the "es-modules" syntax;

#### Module-less typescript

* A TypeScript file is considered module-less if it has no imports or exports;
* All typescript source files share the same global context. Which is defined at the `include` entry of the tsconfig;
* A file can manually include a reference through the addition of the "triple slash directive" at the first line. Shivers from the good-ol-triple-slash-directive-times?

```text
///<reference path=“./path/to/file”/>
```

#### Moduleful typescript

* The TS import syntax comes from the es-module syntax;
* You can also write some additional syntax not covered by the es-modules:

```typescript
import express = require("express") // enforce commonjs import
const express = require("express")  // this works BUT 3rd party types won't get imported
import * as express from 'express'
import express from 'express' // only works with "esModuleInterop"
export = { something: 'x' } // "module.exports =" syntax from commonjs
```

