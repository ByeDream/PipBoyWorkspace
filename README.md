# pip-playground

A runtime environment for [Pip-Boy](https://github.com/ByeDream/Pip-Boy), the personal assistant agent.

## Setup

```bash
# 1. Create a virtual environment
python -m venv .venv

# 2. Activate it
# Windows PowerShell
.\.venv\Scripts\Activate.ps1
# macOS / Linux
# source .venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Configure
# Edit .env and fill in your ANTHROPIC_API_KEY (required)
# See the Pip-Boy README for all available configuration options
```

## Usage

```bash
# Start the agent (auto mode — enables all configured channels)
pip-boy

# CLI-only mode
pip-boy --cli

# Force WeChat QR login
pip-boy --scan

# Show version
pip-boy --version
```

## Updating

From within a running session:

```
/update
```

Or manually:

```bash
pip install --upgrade pip-boy
```

## Configuration

Environment variables are configured in `.env`. See the
[Pip-Boy Configuration](https://github.com/ByeDream/Pip-Boy#configuration) table
for all available options.

## License

This project is licensed under the MIT License.
