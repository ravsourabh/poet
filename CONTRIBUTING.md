# Contributing to Poet - AI Devotional Song Generator

Thank you for considering a contribution! Here's how to get started.

## Getting Started

1. Fork the repository and clone your fork.
2. Copy `.env.example` to `.env` and add your Gemini API key.
3. Install dependencies: `pip install -r requirements.txt`
4. Run a quick test: `python generate_songs_llm.py 1 1`

## How to Contribute

### Bug Reports
Open an issue with:
- Steps to reproduce
- Expected vs actual behavior
- Python version and OS
- Relevant cost report or error output (remove any personal data first)

### Feature Requests
Open an issue describing the use case and expected behavior before writing code.

### Pull Requests
1. Create a feature branch from `main`.
2. Keep changes focused - one concern per PR.
3. Test with at least one song generation end-to-end.
4. Update `README.md` or `COMPLETE_GUIDE.md` if you change behavior or add config options.
5. Open the PR against `main`.

## Code Style

- Follow existing patterns in `generate_songs_llm.py`.
- Add constants to the `Config` class rather than hardcoding numbers.
- Keep prompts in clearly named methods.
- No unnecessary comments - name things clearly instead.

## What Not to Commit

- `.env` files with real API keys
- Generated output (`content/`, `cost_reports/`, `.generation_progress.json`)
- Binary RAG data (`rag_data/`)

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
