# State Management

## What is state management?

When executing an application, we can't store and retrieve values from frame to frame.

To actually store and access data between frames, we need a global application state structure.

In Maycoon, we can use `#[derive(State)]` to automatically implement the `State` trait for a struct.

```rust
#[derive(State)]
struct MyState {
    my_data: MyDataType,
}
```

## Managing a state.

There are multiple implementation for handling application states among different frameworks, but Maycoon uses its own
kind of state management system.

Every value inside a widget (such as a text) should be wrapped inside a `Val<T>` where T is the data type.

The `Val<T>` itself is an enum and has two variants:

- `Val::State { factory, .. }` for state dependent values.
- `Val::Val(T)` for state independent values.

### State dependent values

State dependent means, you need access to the global application `State` to produce a value.

This might be a simple field (`state.value`) or a more complex operation (e.g. retrieving something from a database).

To wrap a state dependent value inside a `State` you can use the `Val::new_state()` function, but we recommend using the `val!()` macro to create a state value like this:

```rust
// simple
val!(|state: MyState| state.counter);

// more complex
val!(|state: MyState| {
    let value = state.input;

    let life = meaning_of_life(value);

    return if life.is_some() {
        "life has meaning".to_string()
    } else {
        "life has no meaning".to_string()
    }
});

// or just using the `new_state` constructor
Val::new_state(|state: MyState| state.counter + 1);
```

### State independent values

State independent means, you do not need to access the global application `State` to produce a value.

This means that you can use literals or other "constants" or simply state independent values.

You can create these values using the `Val::new_val`, the `val!()` macro or simply cast a value into a `Val` like this:

```rust
// constructor
Val::new_val(3);

// `val!()` macro
val!("Hello World".to_string());

// cast `into()` the `Val`
103.into();
```

## State Mutability

When using `Val` to access data, a `State` is always borrowed as immutable variable. This means you only have read-access to the inner value.

If you want to make a widget with mutable state (like an `on_click` handler), you can use a custom `Fn(&mut State)` and call it in your `update` function, when creating a widget.
