# eytzinger-interpolation

[![Crates.io](https://img.shields.io/crates/v/eytzinger-interpolation.svg)](https://crates.io/crates/eytzinger-interpolation)
[![Documentation](https://docs.rs/eytzinger-interpolation/badge.svg)](https://docs.rs/eytzinger-interpolation)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This crate implements the "Eytzinger" (aka BFS) array layout with additional interpolative search support.

## Origin

This is a fork of [rust-eytzinger](https://github.com/main--/rust-eytzinger) by [main()](https://github.com/main--), with additions by [Andre Popovitch](https://github.com/anchpop). The original crate provides excellent performance for binary search operations using the Eytzinger layout.

## Why This Fork Exists

This fork was created to add the `eytzinger_interpolative_search_by` method and related functionality, which enables efficient interpolation between values in an Eytzinger-laid-out array. This is particularly useful for applications like isotonic regression where you need to find values that fall between data points.

The additions were needed for the [pav.rs](https://github.com/sanity/pav.rs) isotonic regression library to achieve optimal performance while maintaining the ability to publish to crates.io (which doesn't support git dependencies).

## What is the Eytzinger Layout?

The Eytzinger layout is a cache-friendly array representation of a binary search tree. Instead of storing elements in sorted order, it arranges them by tree level (breadth-first), which significantly improves binary search performance by reducing cache misses.

For example, a sorted array `[0, 1, 2, 3, 4, 5, 6]` becomes `[3, 1, 5, 0, 2, 4, 6]` in Eytzinger layout.

See ["Array layouts for comparison-based searching" by Khuong and Morin](https://arxiv.org/abs/1509.05053) for detailed performance analysis.

## Features

All features from the original `eytzinger` crate, plus:

- **Interpolative Search**: `eytzinger_interpolative_search_by` returns both the lower and upper bounds around a search value, perfect for interpolation
- Full compatibility with the original API
- Zero-cost abstractions

## Usage

Add this to your `Cargo.toml`:

```toml
[dependencies]
eytzinger-interpolation = "1.0.0"
```

### Basic Eytzinger Search

```rust
use eytzinger_interpolation::SliceExt;

let mut data = [0, 1, 2, 3, 4, 5, 6];
data.eytzingerize(&mut eytzinger_interpolation::permutation::InplacePermutator);

// Now the array is [3, 1, 5, 0, 2, 4, 6]
assert_eq!(data.eytzinger_search(&3), Some(0));
assert_eq!(data.eytzinger_search(&5), Some(2));
```

### Interpolative Search (New!)

The interpolative search returns `(Option<usize>, Option<usize>)` representing the indices of values that bound your search target:

```rust
use eytzinger_interpolation::SliceExt;

let mut data = [0, 1, 2, 3, 4, 5, 6];
data.eytzingerize(&mut eytzinger_interpolation::permutation::InplacePermutator);

// Search for a value between data points
let (lower, upper) = data.eytzinger_interpolative_search_by(|x| x.cmp(&3));
assert_eq!((lower, upper), (Some(0), Some(5))); // Found 3 at index 0, next value at 5

// Interpolate between values
let (lower, upper) = data.eytzinger_interpolative_search_by(|x| (*x as f32).partial_cmp(&3.5).unwrap());
assert_eq!((lower, upper), (Some(0), Some(5))); // 3.5 is between indices 0 (value 3) and 5 (value 4)

// Below range
let (lower, upper) = data.eytzinger_interpolative_search_by(|x| x.cmp(&-1));
assert_eq!((lower, upper), (None, Some(3))); // Below minimum, next value at index 3

// Above range
let (lower, upper) = data.eytzinger_interpolative_search_by(|x| x.cmp(&7));
assert_eq!((lower, upper), (Some(6), None)); // Above maximum, previous value at index 6
```

## Use Case: Isotonic Regression

This crate was created specifically to optimize [pav.rs](https://github.com/sanity/pav.rs), which implements the Pool Adjacent Violators algorithm for isotonic regression. The interpolative search allows efficient lookup and interpolation between regression points.

## Performance

The Eytzinger layout provides significant performance improvements for binary search:

- **Better cache locality**: Forward-only memory access during search
- **Fewer long jumps**: Reduces branch mispredictions at the start of search
- **Hardware prefetching**: Sequential memory access patterns

See the original [rust-eytzinger benchmarks](https://github.com/main--/rust-eytzinger#performance) for detailed numbers.

## Credits

- **Original Author**: [main()](https://github.com/main--) - Created the excellent rust-eytzinger crate
- **Interpolative Search**: [Andre Popovitch](https://github.com/anchpop) - Added interpolative search functionality
- **Maintenance**: [Ian Clarke](https://github.com/sanity) - Published and maintains this fork

## License

MIT (same as the original rust-eytzinger crate)

## Contributing

This fork is primarily maintained to support pav.rs. For general Eytzinger layout improvements, consider contributing to the [upstream rust-eytzinger project](https://github.com/main--/rust-eytzinger).

If you need additional interpolative search features or find bugs in the interpolative search implementation, please open an issue or PR on this repository.

## See Also

- [rust-eytzinger](https://github.com/main--/rust-eytzinger) - The original crate
- [pav.rs](https://github.com/sanity/pav.rs) - Isotonic regression library using this crate
- [Array Layouts Paper](https://arxiv.org/abs/1509.05053) - Academic paper on Eytzinger layouts
