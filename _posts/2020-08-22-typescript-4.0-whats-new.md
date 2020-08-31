---
layout: post
title:  "TypeScript 4.0 Unleashed"
date:   2020-08-22 21:53:23 +0400
categories: angular web development
---

Few Months back [3.8][3.8] and [3.9][3.9] version released which brought type-only imports/exports, along with ECMAScript features like private fields,
top-level `await` in modules, and new `export *` syntaxes, improving the performance and scalability.

#### What's New Summary

What’s New?
Lets dive in to feature Which are most important to Developer Point of View.

- [Variadic Tuple Types] [variadic]
- [Labeled Tuple Elements] [tuple]
- [Class Property Inference from Constructors] [class]
- [Short-Circuiting Assignment Operators] [short]
- [unknown on catch Clauses] [catch]
- [Custom JSX Factories] [jsx]
- [Speed Improvements in `build` mode with `--noEmitOnError`] [speed]
- [\--incremental with \--noEmit][incremental]
- [Editor Improvements] [editor]
    - Convert to `Optional Chaining`
    - `/** @deprecated */` Support
    - Partial Semantic Mode at Startup
    - Smarter Auto-Imports
- [Breaking Changes] [breaking]

### `unknown` on `catch` Clauses

TypeScript 4.0 now lets you specify the type of `catch` clause variables as unknown instead. `unknown` is safer than any because it reminds us that we need to perform some sorts of type-checks before operating on our values.

```javascript
try {
  // ...
} catch (e: unknown) {
  // Can't access values on unknowns
  // error: Object is of type 'unknown'.
  console.log(e.toUpperCase()); 

  if (typeof e === "string") {
    // We've narrowed 'e' down to the type 'string'.
    console.log(e.toUpperCase());
  }
}
```

### Class Properties `Inference` from `Constructors`

TypeScript 4.0 can now use control flow analysis to determine the types of properties in classes when `noImplicitAny` is enabled.

```javascript
class Square {
  // Previously both of these were any
  area;
// ^ = (property) Square.area: number
  sideLength;
// ^ = (property) Square.sideLength: number
  constructor(sideLength: number) {
    this.sideLength = sideLength;
    this.area = sideLength ** 2;
  }
}
```

In cases where not all paths of a `constructor` assign to an instance member, the property is considered to potentially be `undefined`.

```javascript
class Square {
  sideLength;
// ^ = (property) Square.sideLength: number | undefined

  constructor(sideLength: number) {
    if (Math.random()) {
      this.sideLength = sideLength;
    }
  }

  get area() {
    return this.sideLength ** 2;
 // error: Object is possibly 'undefined'.
  }
}
```

In cases where you know better (e.g. you have an initialize method of some sort), you’ll still need an explicit type annotation along with a definite assignment `assertion (!)` if you’re in `strictPropertyInitialization`.

```javascript
class Square {
  // definite assignment assertion
  //        v
  sideLength!: number;
  //         ^^^^^^^^
  // type annotation

  constructor(sideLength: number) {
    this.initialize(sideLength);
  }

  initialize(sideLength: number) {
    this.sideLength = sideLength;
  }

  get area() {
    return this.sideLength ** 2;
  }
}
```

[variadic]: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#variadic-tuple-types
[tuple]: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#labeled-tuple-elements
[class]: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#class-property-inference-from-constructors
[short]: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#short-circuiting-assignment-operators
[catch]: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#unknown-on-catch-clause-bindings
[jsx]: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#custom-jsx-factories
[speed]: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#speed-improvements-in-build-mode-with---noemitonerror
[editor]: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#editor-improvements
[breaking]: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#breaking-changes
[3.8]: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-8.html
[3.9]: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-9.html
[incremental]: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#--incremental-with---noemit