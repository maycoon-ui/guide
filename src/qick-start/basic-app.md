# A Basic Counter App

The easiest way to learn about Maycoon is to start studying some examples. In this Tutorial we will find out how to
create a basic counter App with increase and decrease buttons, as well as a text widget.

## Setup

For creating a new project, see the [Installation Guide](./installation.md).

We need to enable the `macros` feature, which is enabled by default, so you shouldn't worry about it.

## The App

First we need to import the necessary items from the `maycoon` crate:

```rust
use maycoon::core::app::update::Update;
use maycoon::core::app::MayApp;
use maycoon::core::config::MayConfig;
use maycoon::core::layout::{AlignItems, Dimension, Display, FlexDirection, LayoutStyle};
use maycoon::macros::{val, State};
use maycoon::math::Vector2;
use maycoon::widgets::button::Button;
use maycoon::widgets::container::Container;
use maycoon::widgets::text::Text;
```

Now we need a way to store values between frames using a state. You can use `#[derive(State)]` to automatically implement the `State` trait for a struct:

```rust
#[derive(State)]
struct MyState {
    count: i32,
}
```

After that we only need to create the `MayApp` struct with some widgets:

```rust
fn main() {
    MayApp::new(MayConfig::default()).run(
        MyState { count: 0 },
        Container::new(vec![
            Box::new(Button::new(Text::new(val!("Increase"))).with_on_pressed(
                |state: &mut MyState| {
                    state.count += 1;
                    Update::DRAW
                },
            )),
            Box::new(Button::new(Text::new(val!("Decrease"))).with_on_pressed(
                |state: &mut MyState| {
                    state.count -= 1;
                    Update::DRAW
                },
            )),
            Box::new(Text::new(val!(|state: &MyState| state.count))),
        ])
        .with_layout_style(LayoutStyle {
            size: Vector2::<Dimension>::new(Dimension::Percent(1.0), Dimension::Percent(1.0)),
            flex_direction: FlexDirection::Column,
            align_items: Some(AlignItems::Center),
            ..Default::default()
        }),
    );
}
```

A `Container` widget draws and handles a collection of widgets specified as a Vector of `Box`ed Widgets. In our case, we need two buttons: Increase and decrease to manipulate our counter value.

We use the `val!()` macro to automatically create a `StateVal` from an expression.

For the two buttons, we need to define `Update`s to apply updates to the App.

The `Update::DRAW` constant tells the App to only re-draw and not re-layout the App surface.

The `with_layout_style` function applies a custom layout which centers the widgets in our case.

## Running the App

To launch the App, you can run `cargo run`.

If you encounter an error about a stack overflow, you may need to optimize the app using following config:

```toml
[profile.dev]
opt-level = "1"
# Uncomment this if it still doesn't work:
# lto = "thin"
```
