# Number.range

## Status
Author: Nicholas Yang

Stage: -1

## Motivation

Right now, iterating through a range of numbers requires a traditional `for (let i = 0; i < n; i ++)` loop. This is both verbose and not interchangable with other iterators. 

The only way to functionally iterate over a range is to use an array, for instance `Array(n).fill().map((_, i) => console.log(i))`, but that's rather inefficient.

Furthermore, with the iterator helpers proposal, we can use common methods such as `map/filter/reduce` on `Number.range`. This will allow users to write expressions that iterate over a range, which will be very useful cases such as JSX.

## Use cases

**Higher Order Iterators**
Let's say we want to write a higher order iterator that takes in an unspecified iterator, does some transformation and returns a new iterator. The classic example is a map function. Our map function will take a function and an iterator, then return an iterator that applies  the function to each value.

```
function* map(f, iter) {
  for (const val of iter) {
    yield f(val)
  }
}
```

If we try to feed a range of numbers into our map function, we either need to make an array filled with our range, or write our own range implementation.

**Creating n components**

Let's say we want to create 10 Dialog components. Without `Number.range` we'd have to do something like:

```
let dialogs = [];
for (let i = 0; i < 10; i++) {
  dialogs.push(<Dialog />);
}
<div> {dialogs} </div>
```

With `Number.range` (and the iterator helpers methods):

```
<div> {Number.range(0, 10).map(() => <Dialog />).collect()} </div>
```

## Description

`Number.range(start, end, step)` will produce an iterator that iterates from `start` to `end` by adding `step` for each iteration. It will terminate when the index is greater than or equal to end.
