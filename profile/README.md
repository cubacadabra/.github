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
siblings in one parent directory so cross-repository paths such as `../rust`
and `../docs` work as expected.

From the directory where you keep source code:

```sh
mkdir -p cubacadabra
cd cubacadabra

# The GitHub .github repository is checked out locally as dot-github.
git clone git@github.com:cubacadabra/.github.git dot-github

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
  git clone "git@github.com:cubacadabra/${repo}.git" "$repo"
done

# Mark this as the shared multi-repository checkout root and expose the
# organization-wide Codex instructions at its root.
touch .codex-root
ln -s dot-github/AGENTS.md AGENTS.md
```

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
