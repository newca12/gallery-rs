# Spurious stream lock

Without extra care, a simple stream of String can be viciously locked at runtime if not fully UTF-8 compliant.

## Simple stream of String

Does show an error when unvalid UTF-8 line is encountered
```rust,edition2021,no_run
{{#include examples/spurious-stream-lock/string_stream.rs}}
```

Does filter bad lines when unvalid UTF-8 line is encountered
```rust,edition2021,no_run
{{#include examples/spurious-stream-lock/async_string_tokio_stream_nolock.rs}}
```

Does **lock** when unvalid UTF-8 line is encountered
```rust,edition2021,no_run
{{#include examples/spurious-stream-lock/async_string_futures_stream_lock.rs}}
```