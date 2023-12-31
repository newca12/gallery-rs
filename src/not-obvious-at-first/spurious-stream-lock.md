# Spurious stream lock

~~Without extra care, a simple stream of String can be viciously locked at runtime if not fully UTF-8 compliant.~~

> **Update:** This turn out to be a real [bug](https://github.com/rust-lang/futures-rs/issues/2784) in ![futures-0.3.28-badge] and was [fixed](https://github.com/rust-lang/futures-rs/pull/2785)  in ![futures-0.3.29-badge]

## Simple stream of String

Does show an error when unvalid UTF-8 line is encountered
```rust,edition2021,ignore
{{#include examples/spurious-stream-lock/string_stream.rs}}
```

Does filter bad lines when unvalid UTF-8 line is encountered  

[![tokio-badge]][tokio] [![tokio-stream-badge]][tokio-stream]
```rust,ignore
{{#include examples/spurious-stream-lock/async_string_tokio_stream_nolock.rs}}
```

~~Does **lock** when unvalid UTF-8 line is encountered~~  

[![futures-0.3.28-badge]][futures-0.3.28-badge]
```rust,ignore
{{#include examples/spurious-stream-lock/async_string_futures_stream_lock.rs}}
```

{{#include ../links.md}}