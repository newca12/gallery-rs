# Tokio spawn & lifetime

Excerpt from the Tokio [documentation](https://tokio.rs/tokio/tutorial/spawning)  
> When you spawn a task on the Tokio runtime, its type's lifetime must be 'static. This means that the spawned task must not contain any references to data owned outside the task.

Run this to show the compiler error when this requirement is no met.  

[![tokio-badge]][tokio]

```rust,compile_fail
{{#include examples/lifetimes/puzzle1_problem.rs}}
```

The fact that the drop of v after main is not compatible with ```"argument requires that `v` is borrowed for `'static`"``` is not obvious.  
The issue is that v has the lifetime defined by the scope of main() and not the 'static lifetime required by the Trait bound[^ref1] of the spawn function.   

The solution for Tokio API is `Arc`.  

[![tokio-badge]][tokio]

```rust,mdbook-runnable,ignore
{{#include examples/lifetimes/puzzle1_solution.rs}}
```

We can minimize the same issue without Tokio.

```rust,compile_fail
{{#include examples/lifetimes/puzzle1_minimized_problem.rs}}
```

And solved it the same way with `Arc`.

```rust,run
{{#include examples/lifetimes/puzzle1_minimized_solution2.rs}}
```

But why is the Tokio requirement so strong ?  
If the requirement was simply a regular lifetime we can do :

```rust,run
{{#include examples/lifetimes/puzzle1_minimized_solution1.rs}}
```

It turn out[^ref2] that the async executor has exactly this requirement.  
spawn in smol is defined ike this :
```rust,ignore
fn spawn<T: Send + 'a>(&self, future: impl Future<Output = T> + Send + 'a) -> Task<T>
```
whereas Tokio spawn is defined ike this :
```rust,ignore
    pub fn spawn<F>(&mut self, task: F) -> AbortHandle
    where
        F: Future<Output = T>,
        F: Send + 'static,
        T: Send,
```

So I would expect this code to compile :  

[![async-executor-badge]][async-executor]
```rust,ignore
{{#include examples/lifetimes/puzzle1_problem_extended.rs}}
```

[^ref1]: [Lifetime as a trait bound](https://doc.rust-lang.org/rust-by-example/scope/lifetime/static_lifetime.html#trait-bound)  
[^ref2]: [How to deal with tokio::spawn closure required to be 'static and &self?](https://stackoverflow.com/a/69963971)

{{#include ../links.md}}