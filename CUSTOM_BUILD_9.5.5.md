# Combined Advanced Fade + Assisted Highlight Glow - EUI 9.6

Based on official v9.6 (`95316fae767cabfdc990c07de16c30706303f621`).
This existing file name is retained to preserve the combined branch documentation path.

The user reported MANUAL PASS in WoW for the combined 9.6 four-file package on 2026-10-17, with no errors reported. Individual manual scenarios were not itemized. The standalone PR builds were not separately tested in-game.

Installation ZIP SHA-256: `fb184d8b9cdeda9baa8dccf7319d816bf58c9547622c1164793c4bf8599f4388`.
The four feature files match that tested ZIP byte for byte.

Validation: 97 assertions on extracted shipped functions in Lua 5.1, LuaJIT and Lua 5.5; syntax checks of all four files; repository guardrails; git diff checks. luacheck unavailable. Headless checks cannot prove absence of taint in all game states.

Separate upstream PRs:
- #1831: Assisted Highlight Glow, fix/assisted-highlight-glow.
- #1847: Advanced Fade, feat/actionbar-fade-clean.

This combined fork branch is for installation only, without a third upstream PR.
Fork main and stable Releases remain unchanged.
