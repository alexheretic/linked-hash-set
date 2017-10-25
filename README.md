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
use linked_hash_set::LinkedHashSet;
// Type inference lets us omit an explicit type signature (which
// would be `LinkedHashSet<&str>` in this example).
let mut books = LinkedHashSet::new();

// Add some books.
books.insert("A Dance With Dragons");
books.insert("To Kill a Mockingbird");
books.insert("The Odyssey");
books.insert("The Great Gatsby");

// Check for a specific one.
if !books.contains("The Winds of Winter") {
    println!(
        "We have {} books, but The Winds of Winter ain't one.",
        books.len()
    );
}

// Remove a book.
books.remove("The Odyssey");

// Remove the first inserted book.
books.pop_front();

// Iterate over the remaining books in insertion order.
for book in &books {
    println!("{}", book);
}

assert_eq!(
    books.into_iter().collect::<Vec<_>>(),
    vec!["To Kill a Mockingbird", "The Great Gatsby"]
);
```
