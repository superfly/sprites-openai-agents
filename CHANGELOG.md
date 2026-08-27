# Changelog

All notable changes to this project are documented in this file.

## 0.2.0 - 2026-08-27

- Move development and releases from the `superfly/sprites-py` monorepo to
  `superfly/sprites-openai-agents`.
- Expand the tested compatibility range to OpenAI Agents SDK 0.18.2 through
  0.22.x and `sprites-py` 0.3.x through 0.5.x.
- Add minimum-version, latest-supported, and scheduled upstream compatibility
  checks.

## 0.1.0 - 2026-07-20

- Publish the initial Sprites sandbox provider for the OpenAI Agents SDK.
- Support ephemeral and named Sprites sessions, command execution, PTYs,
  filesystem operations, workspace persistence, exposed ports, cloud bucket
  mounts, platform context, URL visibility, and checkpoints.
