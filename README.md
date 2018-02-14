linked\_hash\_set
[![crates.io](https://img.shields.io/crates/v/linked_hash_set.svg)](https://crates.io/crates/linked_hash_set)
[![Documentation](https://docs.rs/linked_hash_set/badge.svg)](https://docs.rs/linked_hash_set)
=================

This library provides an hashed set with predictable iteration order, based on the insertion order of elements.
It is implemented as a [`linked_hash_map::LinkedHashMap`](https://github.com/contain-rs/linked-hash-map) where the value is `()`, in a similar way as `HashSet` is implemented from `HashMap` in stdlib.

## Comparison with std [`HashSet`](https://doc.rust-lang.org/std/collections/struct.HashSet.html)

General usage is very similar to a traditional hashed set, but this structure also maintains **insertion order**.

Compared to `HashSet`, a `LinkedHashSet` uses an additional doubly-linked list running through its entries.
As such methods `front()`, `pop_front()`, `back()` and `pop_back()` are provided.

## Comparison with [`IndexSet`](https://github.com/bluss/indexmap)

Compared to `indexmap::IndexSet`, while both maintain insertion order a `LinkedHashSet` uses a linked list allowing performant removals that don't affect the order of the remaining elements. However, when this distinction is unimportant indexmap should be the faster option.

## Example

```rust
extern crate linked_hash_set;
use linked_hash_set::LinkedHashSet;

let mut set = LinkedHashSet::new();
assert!(set.insert(234));
assert!(set.insert(123));
assert!(set.insert(345));
assert!(!set.insert(123));

assert_eq!(set.into_iter().collect::<Vec<_>>(), vec![234, 345, 123]);
```
