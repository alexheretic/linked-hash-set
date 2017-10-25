linked_hash_set
<a href="https://crates.io/crates/linked_hash_set">
  <img src="http://img.shields.io/crates/v/linked_hash_set.svg">
</a>
<a href="https://docs.rs/linked_hash_set">
  <img src="https://docs.rs/linked_hash_set/badge.svg">
</a>
================

A linked hash set implemented as a `linked_hash_map::LinkedHashMap` where the value is `()`, in a similar way std `HashSet` is implemented from `HashMap`.

General usage is very similar to a std `HashSet`. However, a `LinkedHashSet` **maintains insertion order** using a doubly-linked list running through its entries.
As such methods `front()`, `pop_front()`, `back()` and `pop_back()` are provided.

```rust
extern crate linked_hash_set;
use linked_hash_set::LinkedHashSet;

let mut set = LinkedHashSet::new();
set.insert(234);
set.insert(123);
set.insert(345);
set.insert(123);

assert_eq!(set.into_iter().collect::<Vec<_>>(), vec![234, 345, 123]);
```
