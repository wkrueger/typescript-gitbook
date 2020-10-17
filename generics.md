# Generics

Roughly saying, generics are types which can receive type parameters. Like every other type related feature shown, it does not emit any extra JavaScript output.

```typescript
interface GenericInterface<Data> {
    content: Data
}

type FunctionOf<X, Y> = (i: X) => Y

// functions and classes can also receive type parameters.
function makeData<Input>(i: Input) {
    return { data: i }
}

function cantInfer<Output>(i: any): Output {
    return i
}

class GenericClass<Input> {
    constructor(public data: Input) { }
}
```

* A type parameter can receive a default type, making it optional.

```typescript
function hello<X = string>() {
    return {} as any as X
}
```

#### Argument inference

* A generic function will, at first, require that you supply its type parameters;

```typescript
cantInfer(2) // error
cantInfer<string>(2) //okay
```

* If the type parameter has a default value, it is not required;

```typescript
hello() //ok
hello<Promise>() //ok
```

* If type parameters are referenced in function arguments and NO type parameters are passed on call, TS will try to infer them from the arguments;

```typescript
function makeData<Input>(i: Input) {
    return { data: i }
}
makeData(2) // Input gets inferred to `number`
            // return type is inferred to { data: number }
makeData<string>(2)  // will raise an error since type parameter
                     // and argument are incoherent
```

#### Bounded type parameters

* A type argument can have constraints;

```typescript
function acceptObject<Input extends { x: number }>(i: Input) {
    return i
}
acceptObject({}) // error, must at least have x
acceptObject({ x: 2, y: 3 }) // ok, and returns { x, y }
```

