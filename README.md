# Comma separated field declarations

Champion: Yehuda Katz

First draft author: Daniel Ehrenberg

## Description

In a class declaration, you can define multiple fields separated by `;`. In this proposal, you can use `,` to separate closely related field declarations, which would share decorators and `static`. For example:

```js
class C {
  @reader #x, #y;
}
```

## Risks

The grouping of the decorator and `static` with fields is unclear, especially in conjunction with initializers. For example, in

```js
class C {
  @reader #x = 1 + 2 + 3 + 4,
    #y = 5;
}
```

Here, there are two competing readings: Either a reader could be created for just `#x`, or it can be created for `#x` as well as `#y`.

In code review threads for implementing this feature, a number of people had the reading that it would apply to only one of the comma-separated items, rather than both of them.

## Implementation status

There is a [PR](https://github.com/babel/babylon/pull/608) for this feature in Babel, but it has not landed, awaiting more clarity from TC39.

This sort of feature was [considered](https://github.com/Microsoft/TypeScript/issues/13998) for TypeScript but delayed to ensure there wouldn't be a conflict with JavaScript.
