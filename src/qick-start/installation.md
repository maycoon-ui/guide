# Installation

If you haven't already, you can install the [Rust Programming Language](https://www.rust-lang.org/) using `rustup`.

To create a new cargo project, run `cargo new --bin <project-name>`.

After creating the project, you can `cd` into the folder and then run `cargo add maycoon` to add `maycoon` as a
dependency.

## Feature Gates

Most cargo dependencies have feature gates that toggle special modules. You can add features by editing
the `Cargo.toml` like this:

```toml
[package]
name = "my_project"
description = "My Awesome App"
# other stuff...

[dependencies]
maycoon = { version = "*", features = ["vg"] }
```

### Following features are available at the time of writing:

- `vg` - Enables structures and functions for drawing vector graphics using [vello](https://github.com/linebender/vello).

- `macros` - Enables useful macros for easier development.
