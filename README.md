# Data Structures in C++

Hand-written implementations of common data structures and algorithms in C++,
**without using standard library containers**. Memory is managed manually with
`new[]` / `delete[]`, so every structure is built from scratch.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## About

- Language standard: **C++17**
- Storage: manual memory management via `new[]` / `delete[]`, no `std::vector`, `std::list`, etc.
- Principle: **understand how the data lives in memory before writing code**
- Each structure ships with: header + implementation + unit tests + study notes

## Project Layout

```
DataStructure/
├── docs/          Study notes (one per data structure: complexity, pitfalls)
├── include/       Header files (interface declarations)
├── src/           Implementations (only one main.cpp as a manual driver)
├── test/          Unit tests (one test_*.cpp per data structure)
├── LICENSE
├── README.md
└── .gitignore
```

## Progress

| # | Data Structure | Header | Impl | Test | Notes | Status |
|---|----------------|:------:|:----:|:----:|:-----:|:------:|
| 1 | SeqList | ✅ | ✅ | ✅ | ✅ | Done |
| 2 | LinkedList | ⬜ | ⬜ | ⬜ | ⬜ | Planned |
| 3 | DoublyLinkedList | ⬜ | ⬜ | ⬜ | ⬜ | Planned |
| 4 | Stack | ⬜ | ⬜ | ⬜ | ⬜ | Planned |
| 5 | Queue | ⬜ | ⬜ | ⬜ | ⬜ | Planned |
| 6 | CircularQueue | ⬜ | ⬜ | ⬜ | ⬜ | Planned |
| 7 | BinaryTree | ⬜ | ⬜ | ⬜ | ⬜ | Planned |
| 8 | BST | ⬜ | ⬜ | ⬜ | ⬜ | Planned |
| 9 | Heap | ⬜ | ⬜ | ⬜ | ⬜ | Planned |
| 10 | HashTable | ⬜ | ⬜ | ⬜ | ⬜ | Planned |
| 11 | Graph | ⬜ | ⬜ | ⬜ | ⬜ | Planned |

> ✅ = done, 🚧 = in progress, ⬜ = not started.

## Requirements

| Item | Version |
|------|---------|
| OS | Windows 11 (code itself is cross-platform) |
| Compiler | g++ (MinGW-w64, C++17 support) |
| Editor | Visual Studio Code |

Check the compiler:

```bash
g++ --version
```

If the command is not found, add MinGW's `bin` directory to your system `PATH`.

## Build and Run

No CMake or Makefile. Everything is compiled directly with `g++`.
All artifacts go into `build/`, which is git-ignored.

### Manual driver (src/main.cpp)

```bash
mkdir -p build

g++ -std=c++17 -Wall -Wextra -Iinclude src/main.cpp src/SeqList.cpp -o build/ds.exe

./build/ds.exe
```

> When a new structure is added, append its `src/Xxx.cpp` to the command.

### Run tests

Each test file has its own `main` and is compiled together with its implementation:

```bash
g++ -std=c++17 -Wall -Wextra -Iinclude test/test_seqlist.cpp src/SeqList.cpp -o build/test_seqlist.exe
./build/test_seqlist.exe
```

Passing output:

```
[pass=25 fail=0]
```

On failure, the file name, line number, and failed condition are printed.

### Compile everything at once (PowerShell)

```powershell
mkdir build -Force

g++ -std=c++17 -Wall -Wextra -Iinclude src/main.cpp src/SeqList.cpp -o build/ds.exe

g++ -std=c++17 -Wall -Wextra -Iinclude test/test_seqlist.cpp src/SeqList.cpp -o build/test_seqlist.exe
```

## Conventions

### Naming

| Category | Style | Example |
|----------|-------|---------|
| Header / source files | PascalCase | `SeqList.h` / `SeqList.cpp` |
| Classes / structs | PascalCase | `SeqList` |
| Member variables | `m_` prefix + camelCase | `m_data`, `m_size` |
| Member functions | camelCase | `push_back`, `indexOf` |
| Constants | `k` prefix + PascalCase or ALL_CAPS | `DEFAULT_CAPACITY` |
| Local variables | camelCase | `newCapacity` |

### File structure

Every data structure maps to exactly four files:

```
include/Xxx.h         Interface (what it does)
src/Xxx.cpp           Implementation (how it does it; explicit template instantiation)
test/test_xxx.cpp     Unit tests
docs/Xxx.md           Study notes
```

### Style

- 4-space indent, no tabs
- Opening brace on the same line (K&R)
- Max line length: 100 characters
- Every allocated resource (`new[]`) must be released in the destructor
- Follow the **Rule of Three**: if you write a destructor, you must also write copy constructor and copy assignment

### Memory rules

1. `new` pairs with `delete`, `new[]` with `delete[]`, never mixed
2. On growth: **allocate new memory, move data, then free the old block** — exception-safe
3. Copies are always **deep copies**, avoiding double-free from shared pointers
4. Removal only changes `size`; memory is kept for reuse instead of freed immediately

## Study Notes

Notes for each structure live in `docs/` and cover:

- Memory layout diagram
- Key design trade-offs (why this way, not another)
- Time / space complexity per operation
- Comparison with alternative implementations
- Pitfalls encountered

| Notes | Link |
|-------|------|
| SeqList | [docs/SeqList.md](docs/SeqList.md) |

## Complexity Cheat Sheet

For SeqList as an example:

| Operation | Complexity |
|-----------|------------|
| Access by index `at` / `[]` | O(1) |
| `push_back` / `pop_back` | Amortized O(1) |
| `insert` / `erase` | O(n) |
| `indexOf` / `contains` | O(n) |
| `reverse` | O(n) |

## References

- *Data Structures (C Edition)* — Yan Weimin
- *Introduction to Algorithms* — CLRS
- [cppreference.com](https://en.cppreference.com/) — C++ standard library and language reference

## License

Released under the [MIT License](LICENSE).