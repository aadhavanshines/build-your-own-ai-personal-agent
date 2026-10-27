# Build Your Own AI Personal Agent: the code

This is **Sparrow**, the personal AI agent built step by step in the book *Build Your Own AI Personal Agent: An Always-On Assistant That Chats Where You Do, Remembers, Learns Skills, Works on a Schedule and Runs Safely in a Sandbox, Built and Tested End to End in Python* by Aadhavan Muthurengan, together with its tests and evaluations.

Every file here is the tested file the book prints. If you typed the code from the book, compare your copy with these files, or run the tests against it.

[![Tests](../../actions/workflows/tests.yml/badge.svg)](../../actions/workflows/tests.yml)

## What's here

| Folder | Contents | Chapter |
| --- | --- | --- |
| `sparrow/` | The agent: brain, workspace, tools, memory, skills, gateway, channels, scheduler and the safety layer | 4 to 19 |
| `sparrow/templates/` | The starter workspace: `SOUL.md`, `USER.md`, `AGENTS.md`, `MEMORY.md`, `HEARTBEAT.md` and three skills | 5, 8, 12 |
| `tests/` | 136 unit, functional, security and robustness tests, with a scripted brain and a fake Telegram | 20, 21, 23, 24 |
| `evals/` | End-to-end evaluations with the real model, the system test, the benchmark, and the recorded results | 22, 23, 24 |
| `deploy/` | A systemd user service, a Dockerfile and a run script | 25 |
| `examples/` | The first Agent SDK example | 4 |

## Getting started

You need Linux (or WSL2 on Windows), Python 3.12 or newer, and bubblewrap for the sandbox (Chapter 3).

```
git clone https://github.com/aadhavanshines/build-your-own-ai-personal-agent.git
cd build-your-own-ai-personal-agent
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
sudo apt install bubblewrap        # Debian, Ubuntu, WSL2
```

Run the tests. They need no API key and make no network requests:

```
pytest
```

Then set your Claude API key and start Sparrow (Chapters 3 and 10):

```
export ANTHROPIC_API_KEY="sk-ant-..."
python -m sparrow init
python -m sparrow doctor
python -m sparrow chat             # in the terminal
python -m sparrow run              # web chat (and Telegram, once set up)
```

## Evaluations with the real model

These call the real model and cost money (about US$0.50 for the full run):

```
python evals/run_evals.py          # 16 scenarios, 3 runs each
python evals/system_test.py        # the real process, killed and restarted
python evals/benchmark.py          # Sparrow's own overhead (free, no model)
```

The results recorded for the book are in `evals/results.log`, `evals/results.json`, `evals/system-test.txt` and `evals/benchmark.json`: 48 of 48 real-model runs passed, the system test passed 11 of 11 checks, and Sparrow adds about 8 ms per message.

## Versions

The book was tested with Python 3.12, 3.13, 3.14 and 3.15 and the exact package versions in `requirements.txt`. The Tests workflow runs the test suite on all four versions on every push.

## Notes

- All people, sites and data in the examples are fictional; example web addresses use the reserved `.example` domain.
- Sparrow is not OpenClaw or NemoClaw and is not derived from their code.
- Claude is a trademark of Anthropic, PBC. This project is independent and is not affiliated with, sponsored by, or endorsed by Anthropic, NVIDIA, the OpenClaw project or any other company or project named in the book.

## License

MIT. See `LICENSE`. You may use and adapt Sparrow, its tests and its evaluations for your own work.
