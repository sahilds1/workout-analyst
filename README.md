# workout-analyst

An LLM analytics agent for your Strava workouts and personal training log

A command line tool to fetch Strava activities (by ID, single day, or date range) and analyze them in an interactive chat. The chat is a small agent that can search your running log (`RUNLOG.txt`) for past context

## Setup

Copy `.env.example` to `.env` and fill in your [Strava API app](https://www.strava.com/settings/api) credentials and `OPENAI_API_KEY`. The first run prints an authorization URL; open it, approve, and paste the redirect URL back. Tokens are saved to `~/.strava_tokens.json` and refreshed automatically

The running log is a personal file and is gitignored. Start from the example, which shows the format (each entry begins with a `# ` heading):

```sh
cp RUNLOG.example.txt RUNLOG.txt
```

## Usage

Execute [using `uv` to manage dependencies](https://docs.astral.sh/uv/guides/scripts/) without manually managing environments:

```sh
uv run strava.py --start 2026-07-13 --end 2026-07-19
```

Other ways to select activities, pick a model, or point at a different running log:

```sh
uv run strava.py --id 1234567890
uv run strava.py --date 2026-07-14 -m gpt-5-nano
uv run strava.py --date 2026-07-14 --runlog ~/notes/runlog.md
```

Execute without using uv run by adding the script to your PATH and ensuring it is executable:

```sh
strava.py --start 2026-07-13 --end 2026-07-19
```

Each tool call the agent makes is printed as it happens, e.g. `[tool] search_runlog({'query': 'July 15'})`

## Testing

```sh
uv run --extra dev pytest
```

## License
workout-analyst is licensed under the [Functional Source License, Version 1.1, ALv2 Future License](https://fair.io/licenses/)
