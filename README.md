# Number.range

## Status
Author: Nicholas Yang
Stage: -1

## Motivation

Right now, iterating through a range of numbers requires a traditional `for (let i = 0; i < n; i ++)` loop. This is both verbose and not conducive to composition with iterator methods like `map/filter/reduce`.

The only way to functionally iterate over a range is to use an array, for instance `Array(n).fill().map((_, i) => console.log(i))`, but that's rather inefficient.

## Use cases

**Creating n components**

Let's say we want to create 10 Dialog components. Without `Number.range` we'd have to do something like:

```
let dialogs = [];
for (let i = 0; i < 10; i++) {
  dialogs.push(<Dialog />);
}
<div> {dialogs} </div>
```

With `Number.range`:

```
<div> {Number.range(0, 10).map(() => <Dialog />)} </div>
```

