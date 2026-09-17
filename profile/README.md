<p>
    <p align="center" >
      <img src="https://cubacadabra.com/og-image2.jpg" style="width: 100%; height: auto;">
      <br>
    </p>
</p>

cubacadabra is an open-source project in progress. Our long-term goal is to build a meaningfully better user-generated gaming platform for creators, children, and parents. 

- [Developer](https://developer.cubacadabra.com)
- [Landscape](https://cubacadabra.com/landscape)

## Developer checkout

Cubacadabra is split across multiple repositories. Keep the repositories as
siblings in one parent directory so the multi-repository checkout root and
cross-repository paths work as expected.

From the directory where you keep source code, use a macOS/Linux shell:

```sh
mkdir -p cubacadabra
cd cubacadabra

# The GitHub .github repository is checked out locally as dot-github.
git clone https://github.com/cubacadabra/.github.git dot-github

for repo in \
  android_app \
  backend \
  deployed \
  desktop \
  developer \
  docs \
  examples \
  first-game \
  ios_app \
  rust \
  second-game \
  studio \
  third-game \
  tools \
  web
do
  git clone "https://github.com/cubacadabra/${repo}.git" "$repo"
done
```

### Codex setup

Codex normally treats the nearest `.git` directory as the project root. Because
this checkout intentionally contains many sibling Git repositories, configure
Codex to use `.codex-root` as its project-root marker. Add this to your Codex
configuration, normally `~/.codex/config.toml`:

```toml
project_root_markers = [".codex-root"]
```

Do not add `.git` to this list: a repository such as `web/.git` is closer than
`cubacadabra/.codex-root`, so Codex would stop at the individual repository.

From the `cubacadabra` checkout root, create the marker and shared instruction
link:

```sh
touch .codex-root
ln -s dot-github/AGENTS.md AGENTS.md
```

With that configuration, running Codex from `cubacadabra/web`,
`cubacadabra/rust`, or another sibling repository loads the root `AGENTS.md`
first and then that repository's own `AGENTS.md`, if present.

The resulting layout should look like this:

```text
cubacadabra/
├── .codex-root
├── AGENTS.md -> dot-github/AGENTS.md
├── dot-github/
├── docs/
├── rust/
├── studio/
├── tools/
├── web/
└── ...
```

The `AGENTS.md` symlink makes the organization-wide workflow and architecture
rules available when working in any repository below this checkout. Repository
folders may also contain their own `AGENTS.md` with more specific instructions.
