# What Typescript IS for?

#### Type checking, works like a linter

TypeScript is used as sort of an advanced **linter**, as it points errors in your code based on the coherence of the _data structures_ present in it. I emphasize the term _linter_ here because type-check errors really don't block your code from being compiled. The errors are just there to provide you hints.

In order to collect those data structures, TS uses inference in your code. TS already knows a lot of type data from plain JS alone, but you can also complement those with extra **type annotations**.

> There are a few exceptions of TS features that deviate from the philosophy that "TS is only for type-checking". Those features are mostly from the early ages of TS and they don't want to add more of those. They should be treated as exceptions.
>
> Exemples of those features: Class annotations, namespaces \(don't use them\), non-string enums.

#### JavaScript compilation

As type annotations are not understood by JS parsers, source `.ts` files must be compiled to `.js` in order to remove those. Typescript itself includes a compiler and nowadays this can also be done with Babel.

The TS _language_ aims to keep aligned with JS and proposals that had reached stage 3 \("surely coming to JS"\). TS aims NOT to include extraneous features that are not or won't be part of JS.

So, by writing TS, you are mostly writing a near future version of JS with types. As with Babel, you can then choose which target to compile \(how old is the browser or node.js version you wish to support\).

#### Language services

Language service support is a big focus and differential of TypeScript. A language service is a layer which aims to provide editor goodies like tooltips, navigations, completions, refactors, and suggestions, a dozen of small features which actually bring big improvements in developer experience. The opposite case would be a language in which you only get the compiler feedback when you save a file.

As the TS team works in tandem with the VSCode team to provide its JS language service, its editor experience is very refined.

