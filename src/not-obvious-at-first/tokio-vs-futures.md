# Tokio vs Futures

There are slight but sometimes confusing differences between tokio and the standard library.
[`futures_util::io::AsyncBufReadExt.lines()`](https://docs.rs/futures/0.3.28/futures/io/trait.AsyncBufReadExt.html#method.lines) is an iterator but surprisingly [`tokio::io::util::async_buf_read_ext::AsyncBufReadExt.lines()`](https://docs.rs/tokio/1.32.0/tokio/io/trait.AsyncBufReadExt.html#method.lines) is not.  
Fortunatly [`tokio_stream::wrappers::LinesStream`](https://docs.rs/tokio-stream/0.1.14/tokio_stream/wrappers/struct.LinesStream.html) is a wrapper around [`tokio::io::Lines`](https://docs.rs/tokio/1.28.0/tokio/io/struct.Lines.html) that implements [`Stream`](https://docs.rs/futures-core/0.3.28/futures_core/stream/trait.Stream.html).

## Implementation with Futures
[![async-compression-badge]][async-compression] [![async-fs-badge]][async-fs] [![futures-badge]][futures]
```rust,edition2021,,no_run
{{#include examples/futures.rs}}
```

## Implementation with Tokio
[![async-compression-badge]][async-compression] [![tokio-badge]][tokio]
```rust,edition2021,,no_run
{{#include examples/tokio.rs}}
```

## Implementation with Tokio Stream
[![async-compression-badge]][async-compression] [![tokio-badge]][tokio] [![tokio-stream-badge]][tokio-stream]
```rust,edition2021,,no_run
{{#include examples/tokio_stream.rs}}
```

{{#include ../links.md}}