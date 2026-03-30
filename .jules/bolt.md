# Bolt's Performance Journal - Barebones Browser

This journal tracks critical performance learnings for the Barebones Browser project.

## 2025-05-15 - Redraw Loop Bottleneck
**Learning:** Found an infinite redraw loop in `AnthonyWebView.onDraw()` caused by calling `invalidate()`. This is a classic Android performance anti-pattern that pegs the CPU and drains battery.
**Action:** Always check custom View overrides for recursive `invalidate()` calls. Removed redundant boilerplate overrides to reduce method dispatch overhead.
