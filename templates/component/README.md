# Orbit Extension Template

A starter template for building custom WASM micro-extensions for [Orbit](https://github.com/ziuus/orbit).

## Prerequisites
- Rust and Cargo installed
- `wasm32-unknown-unknown` target installed:
  ```bash
  rustup target add wasm32-unknown-unknown
  ```

## Building
Compile your extension to WebAssembly:
```bash
cargo build --target wasm32-unknown-unknown --release
```
The compiled plugin will be at `target/wasm32-unknown-unknown/release/my_orbit_extension.wasm`.

## Testing Locally
You can test your extension instantly without publishing it:
```bash
# Link the compiled WASM to Orbit
orbit link ./target/wasm32-unknown-unknown/release/my_orbit_extension.wasm

# Start Orbit and configure your layout to use 'my_widget'
orbit
```

## Publishing
To share your extension with the community:
1. Push your repository to GitHub.
2. Publish a GitHub Release containing your `.wasm` file.
3. Open a Pull Request on the [orbit-integrations](https://github.com/ziuus/orbit-integrations) repository to add your extension to the community registry.
