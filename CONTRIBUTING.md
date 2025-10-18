# Contributing to eytzinger-interpolation

Thank you for your interest in contributing to eytzinger-interpolation!

## Scope of This Fork

This fork exists primarily to support the [pav.rs](https://github.com/sanity/pav.rs) isotonic regression library with interpolative search functionality. The scope of this project is intentionally narrow:

- **In scope**: Bug fixes and improvements to interpolative search functionality
- **Out of scope**: General Eytzinger layout improvements (contribute these to [upstream](https://github.com/main--/rust-eytzinger))

## How to Contribute

### Reporting Bugs

If you find a bug in the interpolative search functionality:

1. Check if the issue exists in [upstream rust-eytzinger](https://github.com/main--/rust-eytzinger/issues)
2. If it's specific to interpolative search, open an issue here with:
   - A clear description of the problem
   - Steps to reproduce
   - Expected vs actual behavior
   - Rust version and platform

### Submitting Changes

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass (`cargo test`)
6. Run `cargo fmt` and `cargo clippy`
7. Commit with clear messages
8. Push to your fork and submit a pull request

### Code Style

- Follow standard Rust formatting (`cargo fmt`)
- Address all `cargo clippy` warnings
- Write doc comments for public APIs
- Add examples to doc comments where appropriate

### Testing

- Add unit tests for new functionality
- Ensure doc tests demonstrate real usage
- Test on stable, beta, and nightly Rust when possible

## Relationship with Upstream

This is a friendly fork of [rust-eytzinger](https://github.com/main--/rust-eytzinger). We:

- Credit the original author prominently
- Maintain the same MIT license
- Encourage contributions to upstream for general improvements
- Only maintain this fork for interpolative search features

## Questions?

Open an issue or reach out to the maintainers. We're happy to help!

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
