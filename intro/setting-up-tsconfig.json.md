# Setting up tsconfig.json

Using the TypeScript compiler (`tsc`) is the most simple way to get started. Probably simpler than any Babel-related setup you've ever used. `tsc` can be added to your PATH by globally installing TypeScript (`npm i -g typescript`).

```
tsc -w main.ts
```

... generates a `main.js` file in the same folder with default compiler settings. `-w` toggles the watch mode.

## A simple project

> Below we go through setting tsconfig.json for a simple project compiled using `tsc`. This is mostly commonly used in backend projects. If you are using a predefined build pack like "Create React App", "Next.js" or "Nest.js",
> this already comes set up. Also, those build configurations use javascript bundlers like "Webpack" or "SWC" instead of raw `tsc`.

For a project, it is recommended that you install TypeScript _locally_ so that your project is tied to a specific TS version. In VSCode, `tsc` can be invoked through F1 > Run Build Task. You should also include a link for it in the package.json `scripts`.

`tsc` looks for a `tsconfig.json` file in the same folder. When a `tsconfig` is around, you can just call `tsc` without arguments. The `tsconfig` accepts an overwhelming set of compiler options -- since it mixes compiling and type checking options. Below I'll go through a set of recommended settings.

```
{
  "compilerOptions": {
    ...
  },
  "include: ["src"]
}
```

* `include` filters which files to compile. This can be a folder or an entry point (every file referenced by that entry point will also be compiled);

I will usually split input and output files in different folders:

```
|__ built
| |__ index.js
|__ src
| |__ index.ts
|__ tsconfig.json
```

* By default `tsc` outputs to the same folder the source files are. Use **`"outDir": "built"`** to fix that;

```
  "sourceMap": true
```

* Sourcemaps allow you to debug directly in the source `.ts` files.

```
  "target": "es2017",
  "module": "esnext",
  "esModuleInterop": true
```

Those 3 are output settings:

* `target` dictates how old is the runtime you want to support;
* `module` allows for import/export syntax conversion; You'd usually use "esnext" (no conversion\*) when using a bundler, or "commonjs" for node;
* `esModuleInterop` is an es-modules "quirk" fix;

```
  "strict": true,
  "noImplicitAny": false,
```

Type-checking options:

* `strict` turns on all of the latest type-checking features (very important);
* `noImplicitAny` disables one specially annoying feature with a good trade-off (personal opinion);

```
  "lib": ["dom", "es2015", "es2017"],
```

* `lib`is entirely optional and allows tuning of which global-environment types are available; For instance, the default setting includes "dom", but you'd like to disable "dom" types in a node.js project.

Concluding it, we got:

```
{
  "compilerOptions": {
    "target": "es2017",
    "module": "esnext",
    "esModuleInterop": true,
    "strict": true,
    "noImplicitAny": false,
    "lib": ["dom", "es2015", "es2017"],
    "outDir": "dist",
    "sourceMap": true
  },
  "include": ["src/index.ts"]
}
```
