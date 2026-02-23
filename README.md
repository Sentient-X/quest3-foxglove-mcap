# Quest 3 → Foxglove MCAP Converter

This project converts Quest 3 capture export folders into Foxglove-compatible `.mcap` files.

## Quickstart

1. Install dependencies:

```bash
uv sync
```

2. Convert a capture directory:

```bash
uv run python episode_to_mcap.py --dir data/<capture_dir> --out my_run --res 720x720
```

3. Skip raw image topics (compressed JPEG only):

```bash
uv run python episode_to_mcap.py --dir data/<capture_dir> --out my_run --no-raw
```

## Notes

- Output is written to `out/<name>.mcap`.
- Camera frame input is auto-detected per folder:
  - raw `.yuv` frames (legacy format), or
  - `.jpg` / `.jpeg` frames (new format).
- Supported flags: `--dir`, `--out`, `--res`, `--no-raw`.
- For a full list of options, use:

```bash
uv run python episode_to_mcap.py --help
```
