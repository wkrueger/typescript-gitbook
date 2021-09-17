# More advanced type syntaxes for another day

\(A _veryfast_ reference overview below. Don't worry if you don't understand something, just know that those exist, so you can research later.\)

* _Mapped types_ is a syntax used to declare generic objects.

```typescript
type GenericObject = {
    requireMe: number
    [k: string]: any
}
// GenericObject CAN have any property and MUST have `requireMe`
```

* _Mapped types_  can be used to remap one object type to another, by iterating over its keys.
* `keyof` lists all possible keys of an object type as a type union;

```typescript
type Dummy = {
    a: string
    b: number
}
type Mapped = {
    [k in keyof dummy]: { value: dummy[k] }
}
// wraps Dummy's values into a { value: x } object
```

* Properties may me accessed with `[""]`

```typescript
type X = Dummy['a'] //will return `string`
```

* _Conditional types_ were created to solve a dozen of the type system's limitations. Its name may be misleading. One of the dozen things conditional types can do is to "pick" a type from inside another type expression. For instance:

```typescript
type Unwrap<T> = T extends Promise<infer R> ? R : never
type X = Unwrap<Promise<number>>  // X will be 'number'
// this sample also uses generics, which we will cover soon
```

* The standard type lib includes some auxiliary type aliases like `Record` and `Omit`. All of those type aliases are made by composing the features previously shown.  You can check all available helpers and its implementation by CTRL+Clicking any of them.

```typescript
type DummyWithoutA = Omit<Dummy, 'a'>
```

* `declare` declares a variable for type-checking, without emitting it on JS;

```typescript
declare var Container: Record<string, any>
Container['tiger'] = 'tiger';
// this code will fail on JS but TS compiler won't complain
```

When you want to dig deeper, I'd strongly recommend checking the [Typescript playground samples session](http://www.typescriptlang.org/play/?e=67#example/any).

