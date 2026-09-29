# batchask

Batch prompt runner with real rate limiting and retries

## What it does

- Progress, token counts and a cost estimate on stderr
- Failures go to a sidecar file with error type, message and status
- Per-row overrides for model, system, temperature and max_tokens
- 4xx fails fast; 429 and 5xx retry with jittered backoff
- A bad input line is logged and skipped, never fatal
- Real rate limiting: sliding windows on requests/min and tokens/min
- Idempotent: ids already in the output are skipped on a rerun
- JSONL in, JSONL out: the input is streamed line by line

## Getting started

```bash
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...
```

## How to use

```bash
python batch.py prompts.jsonl -o answers.jsonl --workers 4 --rpm 300
```

## Project structure

```text
├── .github/
│   └── workflows/
│       └── ci.yml
├── docs/
│   ├── development.md
│   ├── faq.md
│   ├── roadmap.md
│   ├── tradeoffs.md
│   └── usage.md
├── tests/
│   └── test_smoke.py
├── .editorconfig
├── .gitignore
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── batch.py
├── prompts.sample.jsonl
└── requirements.txt
```

## Development

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m pytest -q
```

## Why

Needed this for myself; figured others might too.

## License

MIT licensed, see LICENSE.
