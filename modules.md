# Modules

TypeScript is made to adapt to JavaScript. And JavaScript itself has had many module systems for different environments and times. Most notably:

* The browser console "vanilla" environment is module-less. Every imported file lives in the global scope;
* node.js traditionally uses the "commonjs" module syntax;
* Modern front-end code built with module bundlers usually use the "es-modules" syntax;

#### Module-less typescript

* A TypeScript file is considered module-less if it has no imports or exports;
* On a module-less file, variable declarations work in a global context, like you were in a browser environment. The variables you declare on file X will be available on file Y. The TS files are specified in the `include` entry of the tsconfig;

```typescript
// file1.ts
function queryThing(selector: string) {
    return document.querySelector(selector)
}
```

```typescript
// file2.ts
const found = queryThing("table.peoples tr")
// queryThing is globally available
console.log(found)
```

* A file can manually include a reference through the addition of the "triple slash directive" at the first line. This reference will make the types from that file available;

```text
///<reference path=“./path/to/file”/>
```

#### Moduleful typescript

* If a TS file has any `import` or `export`, it is considered "moduleful";
* On "moduleful" files, variable declarations do not add symbols to the global context;
* The TS import syntax for es-modules is similar \(import/export\);
* There is a bit of additional syntax for commonjs imports \(node.js\):
  * Imports are written as `import module = require('module')`
  * The commonjs main export \(`module.exports = {}`\) is written as `export = {}`

```typescript
import express = require("express") // enforce commonjs import
const express = require("express")  // this works BUT 3rd party types won't get imported
import * as express from 'express'
import express from 'express' // only works with "esModuleInterop"
export = { something: 'x' } // "module.exports =" syntax from commonjs
```

**Mixing globals with modules \(advanced\)**

If both a module-less and a moduleful file are in the same workspace:

* The moduleful file will be able to see the globals declared in the module-less file;
* This is often used in library type definitions. Many library typedefs declare globally acessible interfaces \(you don't need to import these interfaces\);
* You can escape the hatch and declare a global type inside a module file through the `declare global` command:

```typescript
// file1.ts
export const name = 'name'

declare global {
  interface GlobalInterface {
    hello: string
  }
}
```

```typescript
// file2.ts
export const dummy = {}

const test: GlobalInterface = {
  hello: 'world'
}
// GlobalInterface is available here
```

**Environment globals**

By default, all browser DOM global types are available in the TS context;

Let's say you are in node.js and you don't want `querySelector` to be a valid global. You can tune it by setting the `lib` key in the `tsconfig`:

```javascript
{
  "compilerOptions": {
    "lib": ["es2017"]
  }
}
```

**EsModuleInterop**

This is a configuration in the `tsconfig`.

```javascript
{
  "compilerOptions": {
    "esModuleInterop": true
  }
}
```

Let's say you are in a node.js environment and `esModuleInterop` turned off. The following import will not work:

```typescript
// this is es-module syntax
import express from 'express`
```

This happens because es-module default import looks for a key named `default` in the module, which does not exist.

The following imports work:

```typescript
import * as exporess from 'express'
import express = require('express')
// ^ will work if tsconfig module = 'commonjs'
```

If you set `esModuleInterop` to `true`, `import express from 'express'` will now work.

