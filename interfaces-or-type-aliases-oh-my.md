# Interfaces or Type Aliases? Oh, my!

* Which one to use? Whatever... both declare types! It is complicated.
* **Type aliases** can receive other things than objects; Most noticeable exclusive to those are:
  * Type unions and intersections;
  * Conditional types;
* **Interfaces** work exclusively with objects \(functions are also objects!\). Exclusive to interfaces are:
  * The OOPish `extends` clause, which is somewhat similar to the type intersection of two objects;
  * **Declaration merging**. When you declare 2 interfaces with the same name, instead of clashing, their properties will merge. \(They can still clash if their properties are incompatible, of course\);
  * Common use of declaration merging: Add another property to the global DOM's `Window` declaration.

```typescript
interface Animal {
    name: string
    isDomestic?: boolean  // optional property, receives type boolean|undefined
    readonly sciName: string  // forbids mutation. Notable sample: react's state
    yell(volume: 1 | 2 | 3 ): void
      //  - types can receive constants (1 | 2 | 3)
      //  - the "void" type is mostly only used in function returns, and
      //    has subtle differences from undefined
    (): void
      // declare this object as "callable" - this is hardly ever used.
    new (): Animal
      // declare this object as "newable" - this is hardly ever used.
}

interface Cat extends Animal {
    isDomestic: true   // narrows down parent's `isDomestic`
    meow(): void;      // additional property
}

// merges with the interface above
interface Cat extends Animal {
    purr(): void
}
```

Type alias sample below. Almost the same capabilities and syntax.

```typescript
type SomeCallback = (i: string) => number
type DiscriminatedUnion = { type: 'a', data: number } | { type: 'b', data: string }

type Animal = {
    name: string
    isDomestic?: boolean
    readOnly sciName: string
    yell(volume: 1 | 2 | 3 ): void
    (): void
    new (): Animal
}

type Cat = Animal & {
    isDomestic: true
    meow(): void
}

// declaration merging not possible
```

