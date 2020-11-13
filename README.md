# ECMAScript Logical Default Assignment

A proposal for using the logical assignments `||=` and `??=` in default assignment in functions arguments and destructuring.

# Examples

```js
// With proposal
function example1_1(arg ??= "some default value") {}
// Without proposal
function example1_2(arg) {
  arg = arg ?? "some default value"
}

// With proposal
function example2_1(arg ||= "some default value") {}
// Without proposal
function example2_2(arg) {
  arg = arg || "some default value"
}

// With proposal
(arg ??= "some default value") => {}
// Without proposal
(arg) => {
  arg ??= "some default value"
}

// With proposal
(arg ||= "some default value") => {}
// Without proposal
(arg) => {
  arg ||= "some default value"
}

// With proposal
const [arg ??= 0] = [null];
// Without Proposal
let [arg] = [];
const arg = arg ?? 0;

// With proposal
const { test ??= 0 } = { test: null };
// Without proposal
let { test: _test } = { test: null };
const test = _test ?? 0;

// With proposal
const [arg ||= 0] = [""];
// Without Proposal
let [arg] = [];
const arg = arg || 0;

// With proposal
const { test ||= 0 } = { test: "" };
// Without proposal
let { test: _test } = { test: "" };
const test = _test || 0;

// Without proposal
const example = ({} = {}, arg) => console.log(arg);
example(null, 1) // ! Error
example(undefined, 1) // 1
// With proposal
const example = ({} ??= {}, arg) => console.log(arg);
example(null, 1) // 1
example(undefined, 1) // 1
```

# Motivation

Along with the motivation provided in the [logical assignment proposal](https://github.com/tc39/proposal-logical-assignment) and the above examples, this further minimizes the syntax for well-known patterns such as function options:
```js
function search({
    depth ||= 1,
    limit ||= 1,
   } ??= {}) {
}
search({ depth: 0 }) // depth and limit are locally scoped in the function as 1
```
This could be particularly useful for unused parameters as given in the final example.


# Semantics

We defer the reader to the semantics provided in the [logical assignment proposal](https://github.com/tc39/proposal-logical-assignment).
