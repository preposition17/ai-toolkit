# Repository Guidelines

This repository contains the AI Toolkit training stack (Python core plus a Next.js UI). Use this guide to orient changes and keep contributions consistent with the current layout and workflows.

## Project Structure & Module Organization
- `toolkit/`: Core Python library (training, data loading, model utilities).
- `config/`: YAML configs and examples (`config/examples/...`).
- `ui/`: Next.js + TypeScript UI, Prisma-backed data, and worker logic.
- `scripts/`: Helper scripts for local workflows.
- `testing/`: Standalone test/diagnostic scripts (run individually).
- `extensions/` and `extensions_built_in/`: Plugin-style modules.
- `assets/`: Images used by docs/UI.
- `output/`, `datasets/`, `jobs/`: Runtime artifacts; avoid committing generated data.
- `docker/` and `docker-compose.yml`: Container and deployment assets.

## Build, Test, and Development Commands
- `python -m venv venv` and `pip install -r requirements.txt`: Set up the Python environment (install the Torch build per README).
- `python run.py config/your_config.yml`: Run a training job from a config.
- `python flux_train_ui.py`: Launch the local Gradio training UI.
- `cd ui && npm run dev`: Start the UI in dev mode.
- `cd ui && npm run build_and_start`: Install deps, migrate Prisma, build, and start the UI on port 8675.
- `cd ui && npm run lint` / `npm run format`: UI linting and formatting.
- `docker compose up`: Start the containerized UI (honors `AI_TOOLKIT_AUTH`).

## Coding Style & Naming Conventions
- Python: 4-space indentation, snake_case for modules/functions, keep config-driven behavior in YAML files under `config/`.
- UI (TypeScript/React): follow existing component structure and use Prettier (`npm run format`) plus `next lint`.
- Prefer descriptive file names and keep new scripts in `scripts/` or `testing/` based on intent.

## Testing Guidelines
- Tests are mostly script-based in `testing/` (e.g., `python testing/test_vae.py`).
- Some utilities include lightweight `unittest` runners (e.g., `python toolkit/image_utils.py`).
- No explicit coverage target is defined; include the command you ran in PR notes.

## Commit & Pull Request Guidelines
- Commits are short, imperative, sentence-case (e.g., "Add LTX-2 support", "Fix UI caption handling"), sometimes with issue refs like `(#123)`.
- PRs should include: a clear description, how to test, linked issues, and screenshots for UI changes.
- Call out any new configs, datasets, or model requirements.

## Security & Configuration Tips
- Store secrets in `.env` (e.g., `HF_TOKEN`) and never commit them.
- Use `AI_TOOLKIT_AUTH` when exposing the UI externally.
- Keep large artifacts in `output/` or `datasets/` and out of version control.
