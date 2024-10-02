# Text

![Hello World example](../assets/hello-world-example.png)

A generic widget that displays a text...

What else is there to say?

See for yourself:

```rust
Text::new("Hello, World!".to_string())
```

or see the "hello-world" example:

```rust
use maycoon::core::app::MayApp;
use maycoon::core::config::MayConfig;
use maycoon::macros::{val, State};
use maycoon::widgets::text::Text;

#[derive(State)]
struct MyState;

fn main() {
    MayApp::new(MayConfig::default())
        .run(MyState, Text::new("Hello, World!".to_string()));
}
```
