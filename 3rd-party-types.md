# 3rd-party types

One can usually obtain types from 3rd party libraries through the following means:

* The library itself publishes `.d.ts` definitions along with the package, referencing it on the `typings` key of package.json;
* Someone publishes types for the library at the _DefinitelyTyped_  repository, available through npm `@types/<lib>`;
* There are methods for manually declaring a 3rd party library's types inside the consumer project;

What if the library does not have types?

* The library will be imported as `any` but you can continue to use it as-is;
* If `noImplicitAny`is turned on, a `declare "library"` entry must be declared in a global file;

3rd party typescript types are also used to power JS type completion in VS Code.
