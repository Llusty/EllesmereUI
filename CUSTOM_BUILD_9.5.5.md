# Combined Advanced Fade + Assisted Highlight review build

Based on upstream source `c1bf767a83801449db10afdadf66f3307d3f5ff2` (9.6.1 metadata), preserving PR history and the split Action Bars architecture. Later upstream changes at publication affect Group Finder/locales only.

Adds opt-in per-bar Advanced Fade: Maximum Opacity, OR-based conditions, separate fade speeds and native Apply to All/Multiple controls. Defaults remain OFF.

## Review fixes

- Port runtime to EUI_ActionBars_Fade.lua and initialization to EUI_ActionBars_Init.lua, using shared internals and the native fader.
- Use native hover/flyout state instead of raw geometric mouseover, preserving empty-slot behavior and flyouts.
- Reapply custom alpha after native Match Any mouseover refresh, including hover-only refreshes; retain Visibility priority and memoize hidden targets.
- Refresh the feature gate before native ApplyAll, so enabling through profile or specialization changes works after starting with Fade disabled, without reload.
- No new polling loop, frame or timer. Hooks install lazily and return at the disabled gate.

Only four feature files: ActionBars main defaults, Fade, Init, and BarVisibilityLayout options. Assisted Highlight remains separate in #1831.

Adds opt-in Assisted Highlight customization using the shared glow engine and native options layout, independent from Custom Proc Glow.

## Review fixes

- Port rendering to EUI_ActionBars_Glows.lua.
- Run custom Assisted glows only in combat; outside combat use the frozen native glow ring.
- Route circle/hexagon buttons through the existing masked ShapeGlow renderer: pulsing color stays within the shape. Square buttons retain the selected custom style, including Pixel Glow.
- Remove the separate legacy style-0 rendering path and selector entry; saved style 0 resolves to the native ring.
- Reuse existing combat synchronization and shared glow helpers. Cache style/color/size/mask to avoid unnecessary restarts, including mask identity changes. No additional events, timers or polling loops.

Only three feature files: ActionBars main defaults, Glows, and AnimationsPage options. Advanced Fade remains separate in #1847.

Validation: repository guardrails and diff checks pass; 30 Lua files compile under Lua 5.1. The combined suite passes 115 assertions plus 8 cold-profile assertions in Lua 5.1, LuaJIT and Lua 5.5. Six mutation controls detect reverted fixes. An audit confirms isolated PR scopes and preservation of native Fade/Init/core behavior after subtracting feature additions, plus unchanged Visibility/state drivers/TOC.

Llusty manually tested the combined build: combat transitions, base/max opacity, Visibility/target conditions, empty-slot mouseover against native behavior, flyout hover, profile switching after reload with Fade disabled, specialization switching ON/OFF without reload, and circle/hexagon masking with return to square pixel glow. No Lua errors were reported. Standalone PR installations were not separately tested; no claim of exhaustive taint testing or performance benchmarking.

Tested combined package SHA-256: `fd15b0efd02e35eee2e1fc375b42179173812de8c2a990651541b0067deb456e`. The six feature Lua files remain identical to tested candidate `98171b62e40c7903532869f5cdb299a923b970de`.

Fork-only installation branch. Existing branch/file names retained; no third upstream PR, official release, or fork main change.
