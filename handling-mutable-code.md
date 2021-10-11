# Handling mutable code

Because of the properties listed before, some patterns that you might be used to in JS may not work well on a static type system. For instance, let's say one would create an object like this:

```typescript
const person = {};
person.name = "John"; // error!
person.lastName = "Wick";
```

TS will complain since `person` is declared by inference to be of type "empty object". Therefore, `person` can't accept any properties.

There are many ways we could adapt our code to tackle this problem. The most recommended one is: build the final object in one step, composing its parts.

```typescript
const person2 = {
  name: "John",
  lastName: "Wick"
}; // OK!
```

Other more verbose way is pre-declaring the object type. This is not ideal though, since we are repeating ourselves.

```typescript
interface Person {
  name?: string;
  lastName?: string;
}
const person3: Person = {};
person3.name = "John";
person3.lastName = "Wick";
```

If you are having a hard time typing something, you can always assign a variable to `any`, disabling all type-checking on it.

```typescript
const person4: any = {};
person4.name = "John";
person4.last.name = "Wick"; // this won't type-error, even if wrong
```

## On the productive use of `any` and other loose types

Every time a developer assigns `any` to a variable, it acknowledges that TS will stop checking it, facing all the consequences this may bring.

While it's not advisable to use `any`, sometimes it can be hard to correctly set the type of a variable, especially when learning the language - or even when facing its limitations. Using `any` is not a crime and sometimes is necessary and productive. One should balance between not using `any` excessively but also not to spend much time trying to fix a type error.
