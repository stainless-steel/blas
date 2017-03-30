# BLAS [![Version][version-img]][version-url] [![Status][status-img]][status-url]

The package provides an interface to the [Basic Linear Algebra
Subprograms][blas].

## [Documentation][documentation]

## Configuration

The underlying implementation of BLAS to compile, if needed, and link to can be
chosen among the following options:

* Apple’s [Accelerate framework][accelerate] (macOS only),
* Netlib’s [reference implementation][netlib], and
* [OpenBLAS][openblas] (default).

An implementation can be chosen using the package’s features as follows:

```toml
[dependencies]
# Apple’s Accelerate framework
blas = { version = "0.15", default-features = false, features = ["accelerate"] }
# Netlib’s reference implementation
blas = { version = "0.15", default-features = false, features = ["netlib"] }
# OpenBLAS
blas = { version = "0.15", default-features = false, features = ["openblas"] }
# OpenBLAS
blas = { version = "0.15" }
```

## Example (C)

```rust
use blas::c::*;

let (m, n, k) = (2, 4, 3);
let a = vec![1.0, 4.0, 2.0, 5.0, 3.0, 6.0];
let b = vec![1.0, 5.0, 9.0, 2.0, 6.0, 10.0, 3.0, 7.0, 11.0, 4.0, 8.0, 12.0];
let mut c = vec![2.0, 7.0, 6.0, 2.0, 0.0, 7.0, 4.0, 2.0];

dgemm(Layout::ColumnMajor, Transpose::None, Transpose::None,
      m, n, k, 1.0, &a, m, &b, k, 1.0, &mut c, m);

assert_eq!(&c, &vec![40.0, 90.0, 50.0, 100.0, 50.0, 120.0, 60.0, 130.0]);
```

## Example (Fortran)

```rust
use blas::fortran::*;

let (m, n, k) = (2, 4, 3);
let a = vec![1.0, 4.0, 2.0, 5.0, 3.0, 6.0];
let b = vec![1.0, 5.0, 9.0, 2.0, 6.0, 10.0, 3.0, 7.0, 11.0, 4.0, 8.0, 12.0];
let mut c = vec![2.0, 7.0, 6.0, 2.0, 0.0, 7.0, 4.0, 2.0];

dgemm(b'N', b'N', m, n, k, 1.0, &a, m, &b, k, 1.0, &mut c, m);

assert_eq!(&c, &vec![40.0, 90.0, 50.0, 100.0, 50.0, 120.0, 60.0, 130.0]);
```

## Contribution

Your contribution is highly appreciated. Do not hesitate to open an issue or a
pull request. Note that any contribution submitted for inclusion in the project
will be licensed according to the terms given in [LICENSE.md](LICENSE.md).

[accelerate]: https://developer.apple.com/reference/accelerate
[blas]: https://en.wikipedia.org/wiki/Basic_Linear_Algebra_Subprograms
[netlib]: http://www.netlib.org/blas
[openblas]: http://www.openblas.net

[documentation]: https://docs.rs/blas
[status-img]: https://travis-ci.org/stainless-steel/blas.svg?branch=master
[status-url]: https://travis-ci.org/stainless-steel/blas
[version-img]: https://img.shields.io/crates/v/blas.svg
[version-url]: https://crates.io/crates/blas
