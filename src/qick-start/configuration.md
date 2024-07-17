# Configuration

You can configure your app using the `MayConfig` struct just like this:

```rust
fn main() {
    let config = MayConfig {
        window: WindowConfig {
            title: "New App".to_string(), // Window Title
            size: Vector2::new(800.0, 600.0), // Window Size
            min_size: None, // Min Window Size
            max_size: None, // Max Window Size
            resizable: true, // If the window is resizeable
            maximized: false, // If the window is maximized on startup
            mode: WindowMode::default(), // The window mode (windowed, fullscreen or exclusive)
            level: Default::default(), // The window level (always top, bottom, normal)
            visible: true, // If the window is visible on startup
            blur: false, // If the background of the window should be blurred
            transparent: false, // If the window background should be transparent
            position: None, // The position (or None if you don't care)
            active: true, // If the window should be active (in focus) on startup
            buttons: WindowButtons::all(), // The enabled window buttons
            decorations: true, // If the window should have decorations/borders
            corners: Default::default(), // The corner configuration
            resize_increments: None, // Optional resize increments
            content_protected: false, // If the content should be protected
            icon: None, // Optional window icon
            cursor: Cursor::default(), // The cursor
            close_on_request: true, // If the window should close when requested via window button
        },
        renderer: RenderConfig {
            antialiasing: AaConfig::Area, // The Anti-Aliasing method
            cpu: false, // If the App should partially use the CPU (still requires a valid GPU) to render
            present_mode: PresentMode::AutoNoVsync, // The buffer presentation mode
        },
        theme: MyAwesomeTheme, // The App Theme
    };

    // your code...
}
```
