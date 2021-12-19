# Imperative vs Declarative

**Declarative programs** we are describing **what** to do, rather than **how** to do it.

### Imperative

```rust
let mut sum = 0;
for i in 1..11 {
    sum += i;
}
println!("{}", sum);
```

### **Declarative**

### Imperative

```rust
let mut sum = 0;
for i in 1..11 {
    sum += i;
}
println!("{}", sum);
```

### **Declarative**

**Declarative programs** we are describing **what** to do, rather than **how** to do it.

```rust
println!("{}", (1..11).fold(0, |a, b| a + b));
```

