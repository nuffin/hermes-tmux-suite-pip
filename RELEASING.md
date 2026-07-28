# Releasing hermes-tmux-suite

Tag-based release — push a `v*` tag to trigger GitHub Actions build + PyPI publish.

## Prerequisites

- Push access to [nuffin/hermes-tmux-suite-pip](https://github.com/nuffin/hermes-tmux-suite-pip)
- [PyPI trusted publishing](https://docs.pypi.org/trusted-publishers/) configured for this repo
- The skill code repo ([hermes-tmux-suite](https://github.com/nuffin/hermes-tmux-suite)) must be pushed first

## Release Steps

### 1. Update skill code (if needed)

If the implement repo (`hermes-tmux-suite`) has new commits, push them first,
then update the submodule:

```bash
cd ~/studio/hermes/projects/hermes-tmux-suite-pip
git submodule update --remote hermes_tmux_suite
cd hermes_tmux_suite && git log --oneline -3  # verify new commits
cd ..
```

### 2. Bump version

Edit `pyproject.toml` → `version = "X.Y.Z"`. Semver rules:

| Change | Bump | Example |
|--------|------|---------|
| Skill feature added | minor | 1.0.5 → 1.0.6 |
| Bugfix only | patch | 1.0.5 → 1.0.6 |
| Breaking change | major | 1.0.5 → 2.0.0 |

### 3. Update CHANGELOG

Add a new section at the top of `CHANGELOG.md`:

```markdown
## vX.Y.Z (YYYY-MM-DD)

- hermes_tmux_suite: <old-hash> → <new-hash>
- feat/fix/docs: <what changed>
```

### 4. Commit

```bash
git add pyproject.toml CHANGELOG.md hermes_tmux_suite
git commit -S -m "chore: bump hermes_tmux_suite + version X.Y.Z"
```

### 5. Tag and push

The tag triggers GitHub Actions → build → PyPI publish:

```bash
git push origin main
git tag vX.Y.Z
git push origin vX.Y.Z
```

### 6. Verify

- GitHub Actions: https://github.com/nuffin/hermes-tmux-suite-pip/actions
- PyPI: https://pypi.org/project/hermes-tmux-suite/
- Test install: `pip install --upgrade hermes-tmux-suite`

## Repository Structure

```
hermes-tmux-suite-pip/
├── pyproject.toml              ← version, package metadata
├── CHANGELOG.md
├── RELEASING.md                ← this file
├── .github/workflows/
│   └── publish.yml             ← tag → build → PyPI
└── hermes_tmux_suite/          ← git submodule (skill code)
    └── skills/
        ├── tmux-delegate-task/
        └── tmux-socket/
```

## Pitfalls

- Push the implement repo **before** updating the submodule — `git submodule update --remote` fetches from origin, not local
- Don't forget the submodule change in the commit — `git status` should show `hermes_tmux_suite` modified
- Existing tags are immutable — if you tagged the wrong commit, use a new patch version
