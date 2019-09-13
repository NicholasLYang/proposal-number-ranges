# Number.range

## Status
Author: Nicholas Yang

Stage: -1

## Motivation

Right now, iterating through a range of numbers requires a traditional `for (let i = 0; i < n; i ++)` loop. This is both verbose and not interchangable with other iterators. 

The only way to functionally iterate over a range is to use an array, for instance `Array(n).fill().map((_, i) => console.log(i))`, but that's rather inefficient.

Furthermore, with the iterator helpers proposal, we can use common methods such as `map/filter/reduce` on `Number.range`. This will allow users to write expressions that iterate over a range, which will be very useful in expression based cases such as JSX.

## Use cases

**Higher Order Iterators**

Let's say we want to write a higher order iterator (or HOI) that takes in an unspecified iterator, does some transformation and returns a new iterator. The classic example is a map function. Our map function will take a function and an iterator, then return an iterator that applies  the function to each value.

```
function* map(f, iter) {
  for (const val of iter) {
    yield f(val)
  }
}
```

`map` can take any generic iterator, allowing it to work over arrays, streams, etc. However it cannot work over a range of numbers unless we pass an array filled with our range, or write our own range implementation. Note that a lot of these higher order iterators will be implemented in the iterator helpers proposal.

**Lazy Streams**

Number ranges also allows for lazy streams of numbers, similar to those of Haskell. For instance, `Number.range(0, Infinity)` is completely valid, as the iterator is lazy itself. 

```
const infinitePosts = map(() => <Post />, Number.range(0, Infinity))
```

**Creating an Array**

Using array spread, it's quite easy to create an array with a range of numbers:

```
const evenNumbers = [...Number.range(0, 100, 2)]
```

## Description

`Number.range(start, end, step)` will produce an iterator that iterates from `start` to `end` by adding `step` for each iteration. It will terminate when the index is greater than or equal to end.

## FAQ

Q: What about `Number.range(-Infinity, Infinity)`/`Number.range(NaN, undefined)`/insert-edgecase-here?

A: The guiding principle of `Number.range(start, end)` is that it is functionally equivalent to a `for (let i = start; i < end; i++)`. While this can lead to some unusual behavior, people already use `for (let i = start; i < end; i++)` loops regularly in codebases and are familiar with their pitfalls.
