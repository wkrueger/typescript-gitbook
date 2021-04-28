# 3rd-party types

One can usually obtain types from 3rd party libraries through the following means:

* The library itself publishes `.d.ts` definitions along with the package, referencing it on the `typings` key of package.json;
  * In this case, the library types will work out of the box. No action needed from you.
* Someone publishes types for the library at the _DefinitelyTyped_  repository, available through npm `@types/<lib>`;
  * In this case, when you import the library, TS will complain it couldn't find type definitions for it. You need to then `npm i @types/that-lib -D`
* There are methods for manually declaring a 3rd party library's types inside the consumer project;

What if the library does not have types?

* The library will be imported as `any` but you can continue to use it as-is;
* If `noImplicitAny`is turned on, a `declare "library"` entry must be declared in global context;
  * Create a `types.ts` without imports and exports in your project, then add `declare "that-library`" to it;

3rd party typescript types are also used to power JS type completion in VS Code.

