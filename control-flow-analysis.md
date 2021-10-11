# Control Flow Analysis

**Definition:**

> At each instruction, a variable's type may be narrowed according to the current context.

```typescript
function cfaSample(x: number|string) {
  console.log(x)  // : number|string
  if (typeof x === 'string') {
    console.log(x) // : string
    return x
  }
  return [x] // [number]
} // inferred return type: string|[number]
```

* Some expressions (`typeof x === 'string'`) act as "type guards", narrowing the possible types of a variable inside a context (the if statement);
* `x` is narrowed from `number|string` to `string` inside the if block;
* `x` only can by `number` at the last line, since the `if` block returns;
* The function gets an inferred return type corresponding to an union of all return paths;

**Discriminated union**

* The type `Actions` below is called a _discriminated union_ . The property `type` is used  as a tag to filter out which of the union options is valid at the context;
* At each `case` line below, `action.data` has its type narrowed down;

```
type Actions =
  | { type: "create"; data: { name: string } }
  | { type: "delete"; data: { id: number } }
  | { type: "read"; data: number }

function reducer(action: Actions) {
  switch(action.type) {
    case 'create':
      return createFoo(action.data) // data: {name: string}
    case 'delete':
      return deleteFoo(action.data) // data: {id: number}
    case 'read':
      return readFoo(action.data)   // data: number
  }
}
```
