# Poet - AI Devotional Song Generator

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/)

Generate high-quality Hindi devotional songs (bhajans, qawwalis, folk songs) using Google Gemini AI with an optimized dual-model pipeline.

**Version 3.0** - 40–50% cheaper, 50% faster, fully reliable.

📖 **[Complete Guide](COMPLETE_GUIDE.md)** - full documentation of all features and configuration  
🗺️ **[Roadmap](ROADMAP.md)** - planned improvements and future tasks

---

## Features

- **Dual-Model Cost Optimization** - Flash for validation, Pro for generation only
- **Iterative Refinement** - fix issues instead of regenerating (saves API cost)
- **Progress Tracking** - resume after crashes with automatic checkpoints
- **Cost Reporting** - real-time visibility into API spend per song
- **Backup Flash Model** - auto-recovery from rate limits
- **3 Separate Quality Thresholds** - Hindi, Singability, Cultural (fine-grained control)
- **30+ Unique Structures** - bhajan, qawwali, folk, meditative, sufi
- **Cultural Validation** - religious sensitivity checks built into the pipeline
- **8-Stage Pipeline** - Analysis → Generation → Quality → Metadata → Validation

---

## Quick Start

### 1. Get a Gemini API Key
Visit **https://aistudio.google.com/app/apikey** and create a free API key.

### 2. Configure
```bash
cp .env.example .env
# Edit .env and set GEMINI_API_KEY=your_key_here
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Generate songs
```bash
# Single song (row 46 in First30Days.xlsx)
python generate_songs_llm.py 46 46

# Range of songs
python generate_songs_llm.py 1 10

# All songs marked in the spreadsheet
python generate_songs_llm.py
```

**Output:**
- Songs → `content/` folder (one `.txt` per song)
- Cost reports → `cost_reports/` folder
- Progress state → `.generation_progress.json` (auto-resumed on restart)

---

## Input Format

Songs are driven by an Excel spreadsheet (`First30Days.xlsx`). Each row represents one song with fields for deity, style, theme, mood, and mantras. See the included spreadsheet for the expected column structure.

---

## Cost & Performance

| Configuration | Cost/Song | Time/Song | Quality |
|--------------|-----------|-----------|---------|
| Dual-model (Flash+Pro) | $0.015–0.025 | 25–40 s | Excellent |
| Single Pro model | $0.080–0.100 | 60–90 s | Excellent |
| Single Flash model | $0.001–0.002 | 20–25 s | Good |

**100 songs with dual-model:** ~$2.00 and ~40 minutes.

---

## Output Files

Each song is saved to `content/day_X_name.txt` and includes:
- Song title and complete lyrics with section tags
- Suno AI style description and YouTube metadata
- Quality scores (Hindi, Singability, Cultural)

---

## Configuration

All settings live in `.env`. Copy `.env.example` to get started. Key options:

| Variable | Default | Description |
|----------|---------|-------------|
| `GEMINI_API_KEY` | - | **Required.** Your Google Gemini API key |
| `USE_DUAL_MODELS` | `true` | Flash for checks, Pro for generation |
| `FLASH_MODEL` | `gemini-2.5-flash-lite` | Model for validation/analysis |
| `PRO_MODEL` | `gemini-2.5-pro` | Model for song generation |
| `HINDI_THRESHOLD` | `8` | Min Hindi quality score (1–10) |
| `SINGABILITY_THRESHOLD` | `7` | Min rhythm/melody score (1–10) |
| `CULTURAL_THRESHOLD` | `7` | Min cultural sensitivity score (1–10) |
| `MAX_QUALITY_RETRIES` | `2` | Regeneration attempts on failure |
| `USE_ITERATIVE_REFINEMENT` | `true` | Refine vs regenerate on failure |

See `.env.example` for the full list with explanations.

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Rate limit on Flash | Backup model auto-switches - check `FLASH_MODEL_BACKUP` in `.env` |
| Content too short | Verify `PRO_MODEL` is set and accessible in your region |
| Hindi 9/10 regenerating | Set `HINDI_THRESHOLD=8` (not 10) in `.env` |
| Cost report shows $0 | Enable `USE_DUAL_MODELS=true` in `.env` |

More help: [COMPLETE_GUIDE.md](COMPLETE_GUIDE.md)

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to report bugs, request features, and submit pull requests.

---

## License

MIT - see [LICENSE](LICENSE).
