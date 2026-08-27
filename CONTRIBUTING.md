# Contributing

## Setup

Use Python 3.10 or newer:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -e '.[dev]'
```

## Verify changes

Run the same checks used by CI:

```bash
python -m pytest
python -m ruff check .
python -m mypy src
python -m build
python -m twine check dist/*
```

Changes to the provider contract should include tests against both the minimum
supported dependency pair and the newest supported OpenAI Agents SDK and
`sprites-py` releases.

## Releases

1. Update `version` in `pyproject.toml` and move the relevant changelog entries
   under a dated release heading.
2. Confirm CI passes on `main`.
3. Push a `vX.Y.Z` tag whose version exactly matches `pyproject.toml`.
4. Confirm the `Publish` workflow succeeds through the protected `pypi`
   environment.

The PyPI project uses Trusted Publishing. The publisher must be configured for
the `superfly/sprites-openai-agents` repository, `publish.yml` workflow, and
`pypi` environment before the first release from this repository.
