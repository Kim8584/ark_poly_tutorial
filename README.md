# Using ark_poly
================

`ark_poly` is a Rust library for working with polynomials, providing efficient and flexible data structures and algorithms for manipulating and evaluating polynomials. In this guide, we'll explore how to use `ark_poly` to create and work with multivariate, multilinear, and univariate polynomials.

## Multivariate Polynomials
-------------------------

A multivariate polynomial is a polynomial in multiple variables. In `ark_poly`, we can create a multivariate polynomial using the `SparsePolynomial` type.

### Example: Creating a Bivariate Polynomial

Let's create a bivariate polynomial `f(x, y) = 1 + 2x + 3y + 4xy`:
```rust
use ark_bls12_381::{Bls12_381, Fr as ScalerField};
use ark_poly::{
    polynomial::multivariate::{SparsePolynomial, SparseTerm, Term},
    DenseMVPolynomial, Polynomial,
};

fn main() {
    // Create terms for the polynomial
    let x_0_y_0 = SparseTerm::new(vec![]);
    let x_1_y_0 = SparseTerm::new(vec![(0, 1)]);
    let x_0_y_1 = SparseTerm::new(vec![(1, 1)]);
    let x_1_y_1 = SparseTerm::new(vec![(0, 1), (1, 1)]);

    // Create the polynomial
    let f = SparsePolynomial::from_coefficients_vec(
        2,
        vec![
            (ScalerField::from(1), x_0_y_0),
            (ScalerField::from(2), x_1_y_0),
            (ScalerField::from(3), x_0_y_1),
            (ScalerField::from(4), x_1_y_1),
        ],
    );

    // Evaluate the polynomial at a point
    assert_eq!(
        f.evaluate(&vec![ScalerField::from(0), ScalerField::from(0)]),
        ScalerField::from(1)
    );
    println!("works fine");
    println!("so here is the poly {:?}", f);
}
