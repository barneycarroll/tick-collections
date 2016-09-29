# tick-collections

TickMap &amp; TickSet are subclasses of Map and Set whose contents are cleared every tick. Useful for eg memoization based on highly volatile data. Another way to think of them is Weak collections with all-but-immediate garbage collection.

This package depends upon compliant native implementations of `class`, `Map` & `Set` - without `class` extension, neither native or any of the popular collection shims can be robustly or uniformly patched. `Promise.resolve` is used internally to clear collections on subsequent ticks of state being set - the internals have no opinion on whether that's a shim or not but obviously if you cannot depend on a runtime guarantee of next tick clearing if the runtime is incapable of reliably queuing tasks to execute in the next tick ;)
