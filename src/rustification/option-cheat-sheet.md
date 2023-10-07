## Option Cheat Sheet

Adapted from [λ Tony's blog λ scala.Option Cheat Sheet](https://web.archive.org/web/20130429013704/http://blog.tmorris.net/posts/scalaoption-cheat-sheet/)

---
**and_then** (aka flatMap in Scala)
```rust.ignore
match option {
     None => None,
     Some(x) => foo(x)
 }
```
This code is equivalent to :  
```rust.ignore
option.and_then(foo)
```
---
**flatten**
```rust.ignore
match option {
     None => None,
     Some(x) => x
 }
```
This code is equivalent to :
```rust.ignore
option.flatten() //(and not unwrap() that would fail for option = None)
```
---
**map**
```rust.ignore
match option {
     None => None,
     Some(x) => Some(foo(x))
 }
```
This code is equivalent to :  
```rust.ignore
option.map(foo)
```
---
**for_each**
```rust.ignore
match option {
     None => (),
     Some(x) => foo(x)
 }
```
This code is equivalent to :  
```rust.ignore
option.into_iter().for_each(foo);
```
---
**is_some**
```rust.ignore
match option {
      None => false,
      Some(_) => true
 }
```
This code is equivalent to :  
```rust.ignore
option.is_some()
```
---
**is_none**
```rust.ignore
match option {
      None => true,
      Some(_) => false
 }
```
This code is equivalent to :  
```rust.ignore
option.is_none()
```
---
**all** (aka forall in Scala)
```rust.ignore
match option {
      None => true,
      Some(x) => foo(x)
 }
```
This code is equivalent to :  
```rust.ignore
option.into_iter().all (|x| foo(x))
```
---
**any** (aka exists in Scala)
```rust.ignore
match option {
      None => false,
      Some(x) => foo(x)
 }
```
This code is equivalent to :    
```rust.ignore
option.into_iter().any (|x| foo(x))
```
---
**or** (aka orElse in Scala)
```rust.ignore
match option {
      None => foo,
      Some(x) => Some(x)
 }
```
This code is equivalent to :  
```rust.ignore
option.or(foo)
```
---
**unwrap_or** (aka getOrElse in Scala)
```rust.ignore
match option {
      None => foo,
      Some(x) => x
 }
```
This code is equivalent to :  
```rust.ignore
option.unwrap_or(foo)
```
---
**filter_map().collect()** (aka toList in Scala)
```rust.ignore
match option {
      None => Vec::new(),
      Some(x) => vec![x]
 }
```
This code is equivalent to :  
```rust.ignore
option.into_iter().filter_map(|x| Some(x)).collect::<Vec<_>>()
```
---
## Resources

[Iterating over an Option](https://rust-unofficial.github.io/patterns/idioms/option-iter.html)