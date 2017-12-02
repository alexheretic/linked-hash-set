# linked\_hash\_set

[![Build Status](https://travis-ci.org/alexheretic/linked-hash-set.svg?branch=master)](https://travis-ci.org/alexheretic/linked-hash-set)
[![crates.io](https://img.shields.io/crates/v/linked_hash_set.svg)](https://crates.io/crates/linked_hash_set)
[![Documentation](https://docs.rs/linked_hash_set/badge.svg)](https://docs.rs/linked_hash_set)

This library provides an hashed set with predictable iteration order, based on the insertion order of elements.
It is implemented as a `linked_hash_map::LinkedHashMap` where the value is `()`, in a similar way as `HashSet` is implemented from `HashMap` in stdlib.

## Comparison

General usage is very similar to a traditional hashed set, but this structure also maintains **insertion order**.

Compared to `HashSet`, a `LinkedHashSet` uses an additional doubly-linked list running through its entries.
As such methods `front()`, `pop_front()`, `back()` and `pop_back()` are provided.

Compared to `ordermap::OrderSet`, a `LinkedHashSet` retains **strict** insertion order and can perform operations (e.g. removals) mid-list in constant time.
Removals are done without affecting the order of the remaining elements.

## Example

```rust
extern crate linked_hash_set;
use linked_hash_set::LinkedHashSet;

let mut set = LinkedHashSet::new();
set.insert(234);
set.insert(123);
set.insert(345);
let new_element = set.insert(123);

assert_eq!(new_element, false);
assert_eq!(set.into_iter().collect::<Vec<_>>(), vec![234, 345, 123]);
```
