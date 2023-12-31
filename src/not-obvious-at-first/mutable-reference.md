## Mutable reference

### A mutable reference can be store in an immutable variable

```rust,ignore
 let mut s = String::from("hello");
 let r1 = &mut s;
```
`r1` is inferred as `&mut String` but using an immutable type is allowed by the compiler and

```rust.ignore
 let r1: &String = &mut s;
```
compile without errors.

Does it compile to the same code if we use immutable reference ?
```rust,ignore
 let r1 = &s;
```

Let's compare
```rust,ignore
pub fn review() {
    let mut s = String::from("hello");
    let r1: &String = &mut s;
    println!("{}",r1);
}
```
and
```rust,ignore
pub fn review() {
    let mut s = String::from("hello");
    let r1 = &s; 
    println!("{}",r1);
}
```
with `cargo-asm asm experiment::review`

As intended the asm code is exactly the same in both cases :
```asm
 push    rbp
 mov     rbp, rsp
 push    rbx
 sub     rsp, 104
 mov     edi, 5
 mov     esi, 1
 call    ___rust_alloc
 test    rax, rax
 je      LBB2_6
 mov     cl, byte, ptr, [rip, +, l_anon.59752abc5bcc54f35c396f0afb4d0f15.1+4]
 mov     byte, ptr, [rax, +, 4], cl
 mov     ecx, dword, ptr, [rip, +, l_anon.59752abc5bcc54f35c396f0afb4d0f15.1]
 mov     dword, ptr, [rax], ecx
 mov     qword, ptr, [rbp, -, 32], rax
 movaps  xmm0, xmmword, ptr, [rip, +, LCPI2_0]
 movups  xmmword, ptr, [rbp, -, 24], xmm0
 lea     rax, [rbp, -, 32]
 mov     qword, ptr, [rbp, -, 40], rax
 lea     rax, [rbp, -, 40]
 mov     qword, ptr, [rbp, -, 56], rax
 lea     rax, [rip, +, __ZN44_$LT$$RF$T$u20$as$u20$core..fmt..Display$GT$3fmt17h75513a3126905787E]
 mov     qword, ptr, [rbp, -, 48], rax
 lea     rax, [rip, +, l_anon.59752abc5bcc54f35c396f0afb4d0f15.3]
 mov     qword, ptr, [rbp, -, 104], rax
 mov     qword, ptr, [rbp, -, 96], 2
 mov     qword, ptr, [rbp, -, 88], 0
 lea     rax, [rbp, -, 56]
 mov     qword, ptr, [rbp, -, 72], rax
 mov     qword, ptr, [rbp, -, 64], 1
 lea     rdi, [rbp, -, 104]
 call    std::io::stdio::_print
 mov     rsi, qword, ptr, [rbp, -, 24]
 test    rsi, rsi
 je      LBB2_4
 mov     rdi, qword, ptr, [rbp, -, 32]
 mov     edx, 1
 call    ___rust_dealloc
LBB2_4:
 add     rsp, 104
 pop     rbx
 pop     rbp
 ret
LBB2_6:
 mov     edi, 5
 mov     esi, 1
 call    alloc::alloc::handle_alloc_error
LBB2_5:
 mov     rbx, rax
 lea     rdi, [rbp, -, 32]
 call    core::ptr::drop_in_place
 mov     rdi, rbx
 call    __Unwind_Resume
 ud2
```
