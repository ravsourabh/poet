# Roadmap & Future Tasks

## Open Source Readiness

The project is ready for open source release with the following in place:
- MIT License
- `.gitignore` excludes `.env`, generated output, API credentials, and runtime artifacts
- No hardcoded API keys - all secrets via `.env`
- `README.md` covers quick start, configuration, and troubleshooting
- `CONTRIBUTING.md` covers bug reports, feature requests, and pull requests

**Before publishing to GitHub:**
- [ ] Replace the sample Excel files (`First30Days.xlsx`, `Next180.xlsx`, `First30DaysVideo.xlsx`) with anonymized or minimal example data, or add them to `.gitignore` if they contain private content plans
- [ ] Verify `rag_data/` is not tracked (already in `.gitignore`)
- [ ] Add a GitHub Actions CI workflow (e.g., `pip install -r requirements.txt` + lint check)

---

## Planned Improvements

### High Priority

- **Cost aggregation** - Weekly/monthly cost summaries rolled up from per-run reports in `cost_reports/`
- **CLI flags** - Replace positional row args with named flags (`--start`, `--end`, `--song-id`) for clarity
- **Better error output** - Structured error log alongside cost report so failures are easy to review post-run
- **Sample data** - Replace private Excel input with a small anonymized example file (`sample_input.xlsx`) so new contributors can run the generator without their own data

### Medium Priority

- **Style-specific structure templates** - Qawwali, folk, meditative each have distinct structural conventions; define them explicitly in `songGuide.md` and pass them through Chain 1
- **Dry-run mode** - `--dry-run` flag that validates the spreadsheet and prints the generation plan without making any API calls
- **Multi-language support** - Extend beyond Hindi to support Urdu, Sanskrit, or regional languages (Marathi, Tamil) with per-language quality thresholds
- **Output formats** - Export to `.srt` (subtitles) or `.pdf` (print-ready sheet music layout) in addition to `.txt`

### Low Priority / Nice to Have

- **Web UI** - Minimal Flask/FastAPI frontend for non-technical users to trigger generation and browse output
- **Cost dashboard** - Parse all files in `cost_reports/` and render a simple HTML chart of cost over time
- **Parallel generation** - Async API calls for the Flash-model validation chains to reduce wall-clock time per song
- **GitHub Actions auto-test** - Smoke test on push using a mock Gemini client to verify the pipeline logic without real API calls

---

## Known Limitations

- LLMs cannot count syllables (matras) accurately - matra-based quality checks are intentionally lenient
- Gemini rate limits vary by tier; the backup Flash model is a workaround, not a fix
- `rag_data/` vector store is pre-built; contributors need to rebuild it locally on first run
