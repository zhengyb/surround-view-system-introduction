# Repository Guidelines

This repository contains a Python-based surround view system with calibration, projection, stitching, and a real-time demo. Use the sections below to develop, test, and contribute effectively.

## Project Structure & Module Organization
- `surround_view/` – core modules (`birdview.py`, `fisheye_camera.py`, `capture_thread.py`, `process_thread.py`, `simple_gui.py`, `utils.py`, `param_settings.py`).
- Scripts – `run_calibrate_camera.py`, `run_get_projection_maps.py`, `run_get_weight_matrices.py`, `run_live_demo.py`, `test_cameras.py`.
- Data – `yaml/` (camera params), `images/` (sample inputs), generated `weights.png` and `masks.png`.
- Docs – `doc/` (detailed walkthroughs, EN/CN).

## Build, Test, and Development Commands
- Install deps (example):
  ```bash
  python -m pip install numpy opencv-python PyQt5 pillow
  ```
- Calibrate camera and save YAML:
  ```bash
  python run_calibrate_camera.py -i 0 -grid 9x6 -o yaml/front.yaml --fisheye
  ```
- Set projection for a view (interactive point picking):
  ```bash
  python run_get_projection_maps.py -camera front -scale 0.7 0.8 -shift -150 -100
  ```
- Compute blending weights and masks:
  ```bash
  python run_get_weight_matrices.py
  ```
- Live demo (update `camera_ids` in script as needed):
  ```bash
  python run_live_demo.py
  ```
- Camera device check (keys: q=quit, s=save, n=next):
  ```bash
  python test_cameras.py
  ```

## Coding Style & Naming Conventions
- Python, PEP 8, 4-space indentation. Use `snake_case` for functions/modules, `CapWords` for classes, `UPPER_CASE` for constants.
- Keep modules focused (match existing file organization). Add docstrings and type hints where they clarify math or I/O.
- Avoid side effects at import; put script entrypoints under `if __name__ == "__main__":`.

## Testing Guidelines
- Existing tests are interactive (camera and demo). Prefer small, testable helpers in `surround_view/`.
- If adding unit tests, place them in `tests/` using `test_*.py` and `pytest` (optional): `pytest -q`.
- Include sample images or clear repro steps when reporting issues.

## Commit & Pull Request Guidelines
- Commits: concise, imperative summaries (e.g., "Add fisheye undistort helper"). No strict convention in history; be descriptive.
- PRs: include purpose, linked issues, run commands, and before/after images (birdview, weights/masks). Update docs if behavior or params change. Keep changes scoped and avoid hardcoded device IDs.

## Security & Configuration Tips
- Verify camera permissions on Linux (membership in `video` group). Device indices vary; adjust in scripts or via args.
