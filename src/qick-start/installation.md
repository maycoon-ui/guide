# Installation

If you haven't already, install the [Rust Programming Language](https://www.rust-lang.org/) using `rustup` or another
way of installing the language.

To create a new cargo project, run `cargo new --bin <project-name>`.

After creating the project, you can `cd` into the project folder and then run `cargo add maycoon` to add `maycoon` as a
dependency.

## Feature Gates

Most cargo dependencies have feature gates that toggle specified features. You can add features by editing
the `Cargo.toml` like this:

```toml
[package]
# ...

[dependencies]
maycoon = { version = "*", features = ["vg"] }
```

### Following features are available at the time of writing:

- `vg`: Enables structures and functions for drawing vector graphics using [vello](https://github.com/linebender/vello).
