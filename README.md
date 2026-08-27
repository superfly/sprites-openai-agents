# Sprites for OpenAI Agents

`sprites-openai-agents` connects [Sprites](https://sprites.dev) to the
[OpenAI Agents SDK](https://developers.openai.com/api/docs/guides/agents/sandboxes)
sandbox interface. It is maintained by the Sprites team and shipped separately
so both `sprites-py` and `openai-agents` remain provider-agnostic.

> [!NOTE]
> The Agents SDK sandbox provider APIs evolve quickly. Each adapter release
> supports an explicitly tested SDK version range.

## Installation

```bash
pip install sprites-openai-agents
```

Set the credentials used by the SDKs:

```bash
export OPENAI_API_KEY=...
export SPRITES_API_TOKEN=...
```

## Usage

```python
from agents.run import RunConfig
from agents.sandbox import SandboxAgent, SandboxRunConfig
from sprites_openai_agents import SpritesSandboxClient

client = SpritesSandboxClient()
sandbox = await client.create()

agent = SandboxAgent(
    name="Sprite assistant",
    instructions="Inspect the workspace and complete the requested task.",
)
run_config = RunConfig(sandbox=SandboxRunConfig(session=sandbox))

async with sandbox:
    # Pass agent and run_config to Runner.run(...) or Runner.run_streamed(...).
    ...
```

By default, the client creates an ephemeral sprite and deletes it when the
session is cleaned up. To attach to an existing sprite:

```python
from sprites_openai_agents import SpritesSandboxClientOptions

sandbox = await client.create(
    options=SpritesSandboxClientOptions(sprite_name="my-sprite"),
)
```

## Development

From the repository root:

```bash
python -m pip install -e '.[dev]'
python -m pytest
python -m ruff check .
python -m mypy src
python -m build
python -m twine check dist/*
```

The adapter uses the public `agents.sandbox` provider contract and must not
import its old in-tree location under `agents.extensions.sandbox.sprites`.

## Compatibility policy

The adapter imports OpenAI Agents symbols from their shortest documented public
path. A few provider primitives—PTY helpers, runtime helper scripts, workspace
path utilities, materialization types, and provider-facing errors—are documented
as modules but are not re-exported from `agents.sandbox`; those imports therefore
remain module-qualified. Upper dependency bounds prevent an untested SDK or
Sprites minor release from silently changing the provider contract.

The CI matrix tests both the minimum supported dependency pair and the newest
versions inside the declared ranges. A scheduled compatibility run also checks
the newest published dependencies so upcoming range updates are visible before
users encounter resolver downgrades.

Development moved from the `superfly/sprites-py` monorepo after version 0.1.0.
The PyPI package name and Python import path did not change.
