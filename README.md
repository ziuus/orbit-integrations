# Orbit Community Integrations 🧩

Official extension registry and templates for [Orbit](https://github.com/ziuus/orbit-tui).

---

## 🚀 Quick Access Tutorial: Using Extensions

Install verified extensions instantly from the command line:

```bash
# 1. Search or browse available extensions
orbit browse

# 2. Install any extension (e.g. 3D Crypto Coin)
orbit install crypto_coin

# 3. Enable in ~/.config/orbit/config.toml
orbit enable crypto_coin
```

Drop the extension's widget ID (e.g. `"coin"`) into your `~/.config/orbit/config.toml` dashboard layout:

```toml
[dashboard]
layout = [
    ["system", "coin", "cpu", "storage"],
    ["clock", "media", "processes", "network"],
    ["weather", "calendar", "upnext", "status"]
]
```

Restart Orbit or press `L` to refresh your layout!

---

## 📁 Ready-to-Use Templates

This repository provides starter templates for every extension type:

| Type | Directory | Description |
| :--- | :--- | :--- |
| **Component (Widget)** | [`templates/component/`](templates/component/) | Rust WASM micro-extension exporting `metadata`, `widgets`, and `render_widget`. |
| **Page (Workspace)** | [`templates/page/`](templates/page/) | Multi-column responsive dashboard layout (`page.toml`). |
| **Theme (Palette)** | [`templates/theme/`](templates/theme/) | Custom 9-color hex palette definition (`theme.toml`). |

---

## 🛠️ Developer Tutorial: Building a Component Extension

### 1. Scaffold from the Template
```bash
git clone https://github.com/ziuus/orbit-integrations
cp -r orbit-integrations/templates/component my-extension
cd my-extension
```

### 2. Implement Your Widget
In `src/lib.rs`:
```rust
use extism_pdk::*;
use orbit_ext_sdk::ui::{span, Block, Color, Line, Style, Widget};

#[plugin_fn]
pub fn render_widget(id: String) -> FnResult<Vec<u8>> {
    let mut lines = Vec::new();
    lines.push(Line::new(vec![
        span("Hello from ", Style::default()),
        span("Orbit WASM!", Style::fg(Color::GREEN).bold()),
    ]));

    let widget = Widget::paragraph(lines).block(Block::titled(" MY WIDGET ".to_string()));
    Ok(widget.to_json())
}
```

### 3. Test Locally in Orbit (No Publishing Needed)
Compile and symlink your widget into your local Orbit configuration:

```bash
cargo build --target wasm32-unknown-unknown --release
orbit link target/wasm32-unknown-unknown/release/my_extension.wasm
```

Add `"my_extension"` to `[extensions] enabled` in `~/.config/orbit/config.toml` and open Orbit.

---

## 🎨 Developer Tutorial: Custom Themes

1. Copy [`templates/theme/theme.toml`](templates/theme/theme.toml) to `~/.config/orbit/themes/neon.toml`.
2. Edit the 9 palette keys:
   ```toml
   bg        = "#140a24"
   accent    = "#ff007f"
   secondary = "#00f5d4"
   surface   = "#221338"
   text      = "#f5e6ff"
   dim       = "#7f6596"
   green     = "#00f5d4"
   yellow    = "#ffbe0b"
   red       = "#ff0055"
   ```
3. In Orbit, press `T` to cycle until your theme activates, or set `ui.theme = "neon"` in `config.toml`.

---

## 📤 Publishing to the Registry

To make your extension available for `orbit install <your_id>`:

1. Fork this repository.
2. Build your `.wasm` binary (`cargo build --target wasm32-unknown-unknown --release`).
3. Compute the SHA-256 hash: `sha256sum my_extension.wasm`.
4. Add your entry to `registry.json`:
   ```json
   {
       "id": "my_extension",
       "name": "My Extension",
       "description": "Short description of what it renders.",
       "version": "0.1.0",
       "api_version": "0.10.0",
       "author": "your_handle",
       "wasm_url": "https://raw.githubusercontent.com/your_handle/my-extension/main/artifacts/my_extension.wasm",
       "sha256": "<computed_sha256_hash>",
       "type": "component",
       "components": [],
       "layout": []
   }
   ```
5. Submit a Pull Request! Once merged, all Orbit users can install it immediately.
