# The primitive types

* All primitive types are referenced in **lowercase**. `number`, `string`, `boolean`, `undefined`, `null`...
* TS adds a couple of extra lowercase types solely related to its type-checking job: `any`, `unknown`, `void`, `never`...
* Arrays can be declared either by `something[]` or `Array<something>`;

> **Be careful:** There also exists an uppercase `Number` type, which is a different thing from lowercase `number`! Types like `Number`, `String`, `Boolean` refer to the **javascript functions** that have those names.
>
> **Be careful:** Both types `{}` and `object` refer to an **empty object**. To declare an object that can receive _any_ property, use `Record<string, any>`.

#### Strict nulls

* Unlike some other languages, types do not implicitly include `null`;
* Ex: in Java, any variable can always also be null;
* In TypeScript a type is declared as nullable through a type union: `type X = Something | null | undefined`
* A type can be narrowed as "not null" through control flow analysis. Ex:

```typescript
const x = 2 as number | null
if (x) {
    console.log(x) // x cannot be null inside this block
}
```

* You can tell the compiler to _assume_ a variable is not null with the `!` operator;

```typescript
interface X {
    optional?: { value: number }
}
const instance: X = {}
console.log(instance.optional.value) // TS will show error
console.log(instance.optional!.value) // assume "optional" exists
```

