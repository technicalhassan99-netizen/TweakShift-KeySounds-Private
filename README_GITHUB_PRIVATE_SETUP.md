# TweakShift Key Sounds — Private GitHub Layout

Recommended repository name:
`TweakShift-KeySounds-Private`

## What to keep in the repository
- `catalog.json` — app-facing metadata/catalog
- `PACK_NAMING_MAP.md` — human-readable mapping
- Optional preview images/audio and documentation

## What to upload as GitHub Release assets
Upload the individual ZIP files from `packs/` to a Release rather than committing all binary packs into normal Git history.

Suggested first release tag:
`key-sounds-v1.0.0`

## Security rule
Do NOT put a GitHub Personal Access Token, GitHub App private key, or any private-repository credential inside the Electron app, React bundle, preload script, native helper, or catalog.

For a private GitHub repository, TweakShift should request a pack from your own backend:
1. App sends pack ID + TweakShift license/session token to your backend.
2. Backend verifies whether the pack is free or premium and whether the user is entitled.
3. Backend authenticates to the private GitHub repository using a server-side GitHub credential.
4. Backend obtains/streams the matching Release asset.
5. App downloads to a `.part` file.
6. App verifies SHA-256 against `catalog.json`.
7. Only after verification does it atomically install the pack.
8. Native audio engine compiles/decodes the selected pack into its local cache and RAM.

Never expose the GitHub credential to end users.
