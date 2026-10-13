# Orbit Theme Extension Template

Themes customize the entire color palette of Orbit dashboards.

## Palette Keys

Every theme TOML file defines 9 hexadecimal color values:
- `bg`: Canvas background
- `accent`: Primary highlight color (borders, gauges, active tabs)
- `secondary`: Secondary accent color
- `surface`: Elevated panel background / card surface
- `text`: Primary readable text
- `dim`: Muted / subtle text and borders
- `green`: Healthy / nominal state
- `yellow`: Warning / medium load
- `red`: Error / critical load

## Testing Your Theme Locally

1. Place your TOML file in `~/.config/orbit/themes/<name>.toml`:
   ```bash
   cp theme.toml ~/.config/orbit/themes/mytheme.toml
   ```
2. Start Orbit and press `T` to cycle until your theme activates, or set `theme = "mytheme"` in `~/.config/orbit/config.toml`.
