> ## Work In Progress

# FLAXOM

<div align="center"><img src="logo.png" alt="blend of one way data flow by global store and decentralizated atoms" align="center"></div>

Event driven state manager with focus on **all** need

- small size (2 KB gziped) and ES5 support
- simple abstraction and friendly DX with minimum boilerplate
- scaling (performance) and modular
- static typed (TS, Flow)
- easy testing
- DI (by functional composition)
- atomic stores (reducers) and subscribtions
- usefull debugging, devtools (redux support)
- declarative and predictable specification of state shape and state mutation
- synchronous glitch free (diamond problem free)
- usefull store fabric (locales, SSR)
- simple integration with other libraries (Observable, etc)
- awkward for write bad code
- handy for write good code

## Example

### Todo-list

[![Todo-list](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/flaxom-todo-app-fikvf)

> Also see tests

## Motivation

> Inspired by redux and effector

### Why not [redux](github.com/reduxjs/redux)

- Selectors are not inspectable (is lacking in devtools)
- Difficult static type inference (because every selector must to know full path to parent state)
- Hard for modular architecture (because every selector must to know about parent state)
- Separation of interfaces, to reducers and selectors, complicating build separated domains
- Selectors - is **manual** API to state. It must be **manualy** described and memorized.
- Selectors execute after state change at subscriptions - error in selector will throw error and is no possibility (ok, all possible, but it is really hard) to restore previous valid state.
- classic reducer API is had much boilerplate and [static] type description boilerplate
- Selectors "runtime" oriented, mean if some "feature" use any part of state (by selector) when you will remove that part, you get the error only when you will try to mount your "feature" at runtime (if you have not static typing). One of the solutions - is connect all features statically by imports.

> A part of problems solves by various fabric functions, but without standardization it is harmful
<!-- - Memorized selectors is extra computations by default, but it is defenetly unnecessary in SSR -->

### Why not [effector](github.com/zerobias/effector)

- Effector is about *atomic stores* - it statefull approach with problems: 1) probable memory leaks 2) difficult [store] instance reusability (for example concurrencies [problems with SSR](https://github.com/zerobias/effector/issues/114)).
  > It can be solved, but better way solve it by design of library architecture and API.
- [Throw in reducer is not cancel computation of other reducers](https://github.com/zerobias/effector/issues/90)

### Why not [MobX](github.com/mobxjs/mobx)
- Huge bundle size and limitation of modern [ES] environment.
- Difficult to use with custom data-structures.
- Runtime semantic and mutable state (is not a better way for debugging).
- [Proxy pattern](https://en.wikipedia.org/wiki/Proxy_pattern) is lack of visual part of code semantic.

### So why single global state?

Immutable data-structures and single entry point for reading and writing are most debuggable things ever (I think). And it most important, because programmer read and debug code much more than write

### Goals

- Reducers may depend from other reducers
- Each reducer must know and react only to depended actions
- Subscribes to reducers
- No glitches
- No breaking changes (at all)

## FAQ

- **Why API so strange, it can't be simpler?**
  > API was designed for bet static types inference (Flow, TS)

## TODO:

- API for `.doNotTrack()` version of reducer for receive it state, but not subscribe to it
- friendly API for work with collections (based on lenses?)
