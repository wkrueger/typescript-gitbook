# Types are spooky! \(How types work?\)

Types live in a separate world set apart from the "concrete variables" world. Think of it as the "upside-down" of types.

If you try to declare both a concrete variable and a type with the same name, they won't clash, since they live in separate worlds.

```typescript
const x = 0;
type x = number; //this is ok!
```

Types are declared by either the `type` or the `interface` statements. While those constructs may have peculiarities in syntax, just consider they are just **ways to declare types**. In the end a type will just represent some structure, regardless of which of the 2 statements you used to declare it\*.

```typescript
interface Animal {
  weight: number;
}
```

The word "interface" may be misleading if you've already used languages like Java or C\#. In TS, an _interface_ just represents a JS object. Which means that any valid JS property can fit in an interface \(not just methods\).

**Types are immutable**

You can't ever modify a type, but you can always create a new type based on another existing one;

```typescript
interface Cat extends Animal {
  isCatnipped: boolean;
}
type MeowingCat = Cat & { meow(): void };
```

On the sample above, we have:

* Created new types based on existing ones;
* We created `Cat` by adding an extra property to `Animal`;
* We created `MeowingCat`by adding an extra property to `Cat`;
* On both cases, we performed a similar operation: _adding an extra property._ We have used 2 different ways to achieve that: `extends` or `type union &` . Both options work fine, you can use any of them.

\*\*\*\*

**A purpose in life**

The final purpose of a type is to be **linked** to a concrete "living" variable. The compiler then compares both to ensure everything is ok.

```typescript
const myFatCat: MeowingCat = {
  weight: 2.4,
  iscatnipped: false, //error!!
  meow() {
    performMeow();
  }
};
```

**What if I don't assign a type to a variable?**

* Every variable will **always** have a type. If I don't explicitly assign a type, the compiler will then infer one from the initial assignment; On VSCode, one can easily check the type of anything by mouse-overing.

```typescript
const barkingFatCat = {
  ...myFatCat,
  bark() {
    throw Error("bark not found");
  }
};
// will have weight, iscatnipped, meow and bark properties
```

> An important advice about working with typescript: **\*\*mouseover everything\*\***. Every variable. Every time. Extensively.
>
> You can do a lot of "debugging" just by carefully inspecting every variable's inferred type.

**A lifelong link**

* **One variable can only have one type during its whole lifespan.** However, you can still create new variables and do casts;

**Going the other way**

* The inverse operation -- retrieving a type from a variable -- is possible with the `typeof` statement. `type StrangeCat = typeof barkingFatCat`.

