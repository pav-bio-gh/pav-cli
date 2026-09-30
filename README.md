# pav: the Pav API from your terminal

[![fern shield](https://img.shields.io/badge/%F0%9F%8C%BF-CLI%20generated%20by%20Fern-brightgreen)](https://buildwithfern.com?utm_source=github&utm_medium=github&utm_campaign=readme&utm_source=Pav%20Enterprise%20API%2FCLI)

Command-line client for the [Pav API](https://docs.pav.bio): biopharma programs, drugs, companies, trials, deals, patents and FDA records. Every resource is `pav <resource> list` and `pav <resource> get`.

This repository is generated from the API's OpenAPI spec; do not edit it by hand.

## Table of contents

- [Installation](#installation)
- [Authentication](#authentication)
- [Quick start](#quick-start)
- [Usage](#usage)
- [Documentation](#documentation)
- [Advanced](#advanced)
  - [Common flags](#common-flags)
  - [Environment variables](#environment-variables)
  - [Output formats](#output-formats)
  - [Shell completion](#shell-completion)
- [Attribution](#attribution)

## Installation

### Shell (macOS / Linux)

```bash
curl -LsSf https://pav.bio/install.sh | sh
```

### PowerShell (Windows)

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://pav.bio/install.ps1 | iex"
```

Installs `pav` to `~/.local/bin`. Release archives for every platform are on the [releases page](https://github.com/pav-bio-gh/pav-cli/releases).

Installs `pav` to `~/.local/bin`. Archives for every platform are on the [releases page](https://github.com/pav-bio-gh/pav-cli/releases).

### Build from source

If you prefer to build from source, install the [Rust toolchain](https://rustup.rs/) and run:

```bash
cargo build --release
./target/release/pav --help
```

## Authentication

Set the following environment variable(s) before using the CLI:

```bash
export PAV_API_KEY="<your_api_key>"   # or: pav auth login (stores it in your OS keychain)
```

A `.env` file in the working directory is also supported — the CLI auto-loads it on startup.

## Quick start

List available commands:

```bash
pav --help
```

Call an API endpoint:

```bash
pav <resource> <method>
```

Run `pav <resource> --help` to see available methods for a resource.

## Usage

Every API resource appears as a subcommand (e.g. `pav <resource> <method>`). Run `pav <resource> --help` to see available methods.

Provide request parameters as flags or as JSON:

```bash
pav <resource> <method> --json '{"key": "value"}'
```

## Documentation

See [reference.md](./reference.md) for the full command reference.

## Advanced

### Common flags

These flags are available on every operation:

| Flag | Description |
|------|-------------|
| `--dry-run` | Validate the request locally and print the HTTP request without sending it |
| `--json <JSON\|->` | Supply a request body as JSON (or `-` to read stdin) |
| `--params <JSON>` | Merge extra parameters as JSON (overrides individual flags) |
| `--format <json\|table\|yaml\|csv>` | Output format (default `json`) |
| `--output <PATH>` | Write binary responses to a file |
| `--base-url <URL>` | Override the API base URL |
| `--no-extract` | Print the full response body instead of the `x-fern-sdk-return-value` extraction |
| `--no-retry` | Disable retries declared by `x-fern-retries`, including network errors |
| `-q, --quiet` | Suppress stdout output on success (errors still go to stderr) |

Operations the spec describes how to page (via `x-fern-pagination` or a root `page_token` parameter) also accept:

| Flag | Description |
|------|-------------|
| `--page-all` | Auto-paginate and stream results as NDJSON |
| `--page-limit <N>` | Max pages to fetch when auto-paginating (default `10`) |
| `--page-delay <MS>` | Delay between page fetches in milliseconds (default `100`) |
| `--no-pager` | Disable the pager even on interactive terminals |

Operations the spec marks as streaming (via `x-fern-streaming`) also accept:

| Flag | Description |
|------|-------------|
| `--no-stream` | Buffer the streaming response and print it as a single value once complete |

### Environment variables

| Variable | Description |
|----------|-------------|
| `PAV_BASE_URL` | Override the API base URL |
| `PAV_CA_BUNDLE` | Path to PEM file with extra trust roots (or `SSL_CERT_FILE`) |
| `PAV_INSECURE=1` | Skip TLS verification (debugging only) |
| `PAV_PROXY` | HTTP(S) proxy URL |
| `PAV_TIMEOUT_SECS` | Total request timeout in seconds |

Standard environment variables (`HTTPS_PROXY` / `HTTP_PROXY` / `NO_PROXY` / `SSL_CERT_FILE`) are also honored.

### Output formats

Use the global `--format` flag to control output. Supported values: `json`, `table`, `yaml`, `csv`, `jsonl`, `raw`, `http`.

Without `--format`, output (including errors) is `table` when stdout is a terminal and `json` when it is piped or redirected — so scripts and agents get JSON by default. Pass `--human` to keep the interactive rendering when piping to a pager, and `--format json` to pin JSON in a terminal.

```bash
# Pipe JSON output through jq
pav <resource> <method> --format json | jq

# Keep the human rendering even when piped
pav <resource> <method> --human | less

# Machine-readable catalog of every operation (same as --schema)
pav --help --format json | jq '.operations | length'
```

### Shell completion

Generate shell completion scripts:

```bash
pav completion <bash|zsh|fish|powershell>
```

## Attribution

Built on [fern-cli-sdk](https://github.com/fern-api/fern), Copyright Fern, licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).

