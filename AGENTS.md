# Repository Guidelines

## Project Structure & Module Organization
This repository is a small Python CLI for converting Quest 3 capture exports into Foxglove-compatible MCAP files.

- `episode_to_mcap.py`: converter entrypoint and CLI (`--dir`, `--out`, `--res`, `--no-raw`).
- `data/`: local input capture data (ignored by git).
- `out/`: generated `.mcap` outputs (ignored by git).
- `axes_yz_swap.md`: coordinate-frame rationale used by the transform logic.
- `pyproject.toml` and `uv.lock`: dependency and environment definition.
- `slam/`: optional subpackage present in the repository but not part of the default converter workflow.

## Build, Test, and Development Commands
- `uv sync`: install/update dependencies from `pyproject.toml` and `uv.lock`.
- `uv run python episode_to_mcap.py --help`: view CLI options.
- `uv run python episode_to_mcap.py --dir data/<capture_dir> --out my_run --res 720x720`: run a conversion and write `out/my_run.mcap`.
- `uv run python episode_to_mcap.py --dir data/<capture_dir> --out my_run --no-raw`: generate compressed-image topics only.
- `uv run python -m py_compile episode_to_mcap.py`: quick syntax validation.

## Coding Style & Naming Conventions
- Follow PEP 8 with 4-space indentation and clear, short helper functions.
- Use `snake_case` for functions/variables and descriptive argument names.
- Keep topic names and frame IDs explicit (for example `"/camera/left/image"` and `"camera_left"`).
- Prefer small, testable functions for parsing, transforms, and message writing.

## Testing Guidelines
No formal test suite exists yet. For each change:
- run `uv run python -m py_compile episode_to_mcap.py`;
- run one end-to-end conversion on a representative dataset in `data/`;
- verify a new file appears under `out/` and that expected topics are present in Foxglove.

When adding tests later, place them under `tests/` and name files `test_<module>.py`.

## Commit & Pull Request Guidelines
- Use Conventional Commit style observed in history: `feat: ...`, `chore: ...`.
- Keep commits focused and functional (one logical change per commit).
- PRs should include: purpose, key behavior changes, commands run for validation, and sample output path(s) (for example `out/<name>.mcap`).
- Link related issues and include screenshots only when visualization behavior changes.
