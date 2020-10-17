# Structural typing

**Definition:**

> In order to determine if two types are assignable, the compiler exhaustively compares all their properties.

This contrasts with _nominal typing_, which works like:

> Two types only are assignable if they were created from the same constructor OR from an explicitly related constructor. \(explicitly related usually means: extends or implements\).

Given two classes A and B:

```typescript
class A {
    name
    lastName
}

class B {
    name
    lastName
    age
}
```

Now let a function require A as input.

```typescript
function requireA(person: A) {}
requireA(new A()) //ok
requireA(new B()) //ok
requireA({ name: 'Barbra', lastName: 'Streisand' }) //ok
requireA({ name: 'Barbra', lastName: 'Streisand', age: 77 }) //error
```

* The function accepted B as input since its properties were considered assignable;
* This would not be allowed on _nominal typing_, since it would require `B` to explicitly `extend` or `implement` `A`;
* Since we are just comparing properties, just directly passing a conforming object also works;
* The last line errors because TS applies a special rule which enforces _exact properties_ if the argument is a literal;

