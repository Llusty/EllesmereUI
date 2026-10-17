# Combined Advanced Fade and Assisted Highlight Glow — EUI 9.5.5

This fork-only branch combines the independent changes from PR #1831 and PR
#1847. It is not a third upstream pull request or a separate addon. Upstream
9.5.5 (`2e23e868593762c256ee84823851c1a280640cd4`) is merged into both PR branches.
Only four Lua files differ from that base, plus this build note.

The four Lua files are byte-for-byte identical to the combined 9.5.5 ZIP for
which the user reported an overall manual in-game PASS on 2026-10-17. Individual
manual scenarios and the WoW client build were not supplied; this does not assert
separate PASS results for every bar type, restricted context or taint scenario.
The two standalone PR builds did not receive separate in-game acceptance tests.

Validation: Lua 5.1/5.5 syntax on the four changed files; 78 function-level
assertions run under Lua 5.1, LuaJIT and Lua 5.5; upstream guardrails; feature
isolation checks for the individual PRs; exact combined-package equality.
Assisted matching rejects secret IDs before comparison. Advanced Fade reads
EUI's own alpha ledger and rejects secret condition states before branching.

Install this fork build OR the four replacement files over full official EUI
9.5.5. Disable the separate LlustyActionBarsExtensions prototype. Use the native
Action Bars settings panels. Updating official EUI can overwrite these changes.
Fork main is unchanged. No third upstream PR, stable tag or GitHub release.
