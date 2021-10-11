# What Typescript is NOT for?

> Writing OOP-styled code like C# or Java;

As TS is mostly "JS with types", you should just write TS as you would write JS, whatever code style you prefer. As classes are a JS feature, you could already write _classy_ code in plain JS.

> Making my code verbose, littered with type annotations;\
> Force me into writing in OOP style;

Since it is made to fit already existing JS patterns, TS's type system is quite flexible. The type system does not strongly dictate what patterns you should use. This, paired with the heavy use of inference allows for the usual TS code to have a small amount of type annotations.

Due to the nature of _static typing_, you will eventually need to adapt some dynamic patterns or lean to more functional patterns, but those will be tiny and beneficial changes. More info on that ahead.

**Real cons of using TypeScript**

Setting up TS in modern frontend projects (webpack-based) used to be a pain. This has changed drastically since the Babel integration came, along with support on popular templates like create-react-app. Community support in this area has now raised a lot, bringing goodies like better library typings.
