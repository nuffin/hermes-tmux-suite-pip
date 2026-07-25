# hermes-tmux-suite

[![PyPI](https://img.shields.io/pypi/v/hermes-tmux-suite)](https://pypi.org/project/hermes-tmux-suite/)

Pip-installable tmux-integrated delegate_task tailing for [Hermes Agent](https://github.com/NousResearch/hermes-agent).

## Install

```bash
pip install hermes-tmux-suite
```

## What's Inside

1 skill bundled from [hermes-tmux-suite](https://github.com/nuffin/hermes-tmux-suite):

| Skill | What it does |
|-------|-------------|
| `tmux-delegate-task` | Dispatch subagent + auto-tail live transcript in tmux pane with auto-cleanup |

## Usage

After install, add the skills directory to your skill-graph config:

```yaml
skills:
  config:
    skill-graph:
      source_dirs:
        - ~/.hermes/skills/devops/
```

Then in Hermes:

```
> 在当前窗口用 tmux-delegate-task 抓取 baidu.com
```

The agent dispatches the subagent, opens a tmux pane with `tail -f` on the live
transcript, and auto-closes the pane when done.

## Repositories

| Role | Repo | PyPI |
|------|------|------|
| Skill code | [hermes-tmux-suite](https://github.com/nuffin/hermes-tmux-suite) | — |
| Pip wrapper (this repo) | [hermes-tmux-suite-pip](https://github.com/nuffin/hermes-tmux-suite-pip) | [hermes-tmux-suite](https://pypi.org/project/hermes-tmux-suite/) |
