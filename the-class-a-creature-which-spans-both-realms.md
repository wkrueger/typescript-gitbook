# The \`class\`, a creature which spans both realms

Classes in TypeScript have a few extra features compared to JS classes, mostly related to type-checking.

* You can declare uninitialized properties on the class body; Those don't generate JS code, they just declare types for checking.
* If a property is not initialized on the constructor, or directly, TS will complain. You can either declare a property as optional (append `?`) or assume it is not null (append `!`).

```typescript
class Foo {
    constructor(name: string) {
        this.name = name
    }
    name: string
    hasBar?: string
    certainlyNotNull!: number
}
```

* Access modifiers (`private`, `protected` and `public`) are a thing; Yet again, they only serve as hints to the type-checker. A `private` declared property will still be emitted and visible in JS code.
* Class fields can be initialized in-body (same as JS, recent-y proposal);

```typescript
class Foo {
    // ...
    private handleBar() {
        return this.name + (this.hasBar || '')
    }
    init = 2;
}
```

* Unique to TS, you can add modifiers to constructor parameters. This will act as a shorthand that copies them to a class property.

```typescript
class Foo {
    constructor(private name: string) {} // declares a private property "name"
}
```

**Both worlds**

The `class` statement differs from most others are it declares _both_ a variable and a type. This is due to the dual nature of JS/OOP classes (a class actually packs 2 objects inside one definition).

```typescript
class Foo {}
type X = Foo          // "Foo - the type" will have the INSTANCE type
type Y = typeof Foo   // Y will have the PROTOTYPE type
                      // (when writing typeof, "Foo" refers to the "living foo",
                      // which in turn is the prototype)
type Z = InstanceType<Y>  // the inverse operation
var foo = new Foo()   // "Foo" exists in both worlds;
```
