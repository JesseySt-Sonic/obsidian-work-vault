# Build your own Git in Rust

A two-for-one project: demystify how git works internally while learning Rust's ownership model, memory allocation, and systems programming concepts.

## Why this combination works well

Git's internals map naturally onto Rust concepts:
- **Content-addressable object store** → teaches file I/O, byte manipulation, and `Vec<u8>` vs `&[u8]` (owned vs borrowed)
- **SHA hashing blobs/trees/commits** → teaches working with external crates (`sha1`, `flate2`)
- **The index (staging area)** → teaches struct design and serialisation/deserialisation
- **Ref following (`HEAD` → branch → commit)** → teaches Rust's `Result`/`Option` chaining and error handling without exceptions

## What to build (in order)

1. `git init` — create `.git/` directory structure. First taste of `std::fs`.
2. `git hash-object` — SHA-hash a file and write it to `.git/objects/`. Teaches byte slices, zlib compression.
3. `git cat-file` — read an object back. Teaches parsing raw bytes into structs.
4. `git write-tree` / `git read-tree` — tree objects. Teaches recursive data structures and lifetimes.
5. `git commit-tree` — commit objects. Teaches string formatting and UTC timestamps.
6. `git log` — walk the commit DAG. Teaches ownership when traversing linked structures.
7. `git add` / `git status` — the index. The hardest part; teaches binary file format parsing.
8. `git checkout` — restoring files from a tree. Teaches filesystem interaction at scale.

## Rust concepts you'll hit naturally

| Concept | Where you'll hit it |
|---|---|
| Ownership & borrowing | Passing byte slices between functions |
| Lifetimes | Tree nodes that reference parent data |
| `Result<T, E>` error handling | Every file read/write |
| Traits (`Display`, `From`, `TryFrom`) | Object type conversions |
| Enums with data | `GitObject::Blob(Vec<u8>)` vs `GitObject::Tree(...)` |
| Memory layout | Understanding why `String` vs `&str` matters |
| `Box<T>` / `Rc<T>` | Recursive commit/tree structures |

## Good resources to pair with this

- [Write yourself a Git — Mary Rose Cook](https://maryrosecook.com/blog/post/git-from-the-inside-out) — Python but the concepts translate directly
- [The Git Book — Chapter 10 (Git Internals)](https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain) — the authoritative object format reference
- [The Rust Book](https://doc.rust-lang.org/book/) — read chapters on ownership, enums, and error handling first

## Related

- [[Build your own CI-CD]] — once you have a working git, wiring up hooks is the natural next step
