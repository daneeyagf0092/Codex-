# QA inventory

## User-visible claims

1. The home screen matches the “灵感小宇宙” mood: cream paper, mint/coral/yellow/blue accents, playful ENFP stationery details, native Codex suggestion cards, and a skinned native composer.
2. The sidebar is warm paper with mint/yellow selection states rather than merely changing the accent color.
3. All real Codex controls remain interactive; the skin is CSS decoration rather than a screenshot overlay.
4. The skin survives route changes and renderer reloads while the injector daemon runs.
5. The official Store package and `app.asar` remain unchanged.
6. Restore removes the injected DOM/CSS and install/restore can be repeated.

## Functional checks

- Home feature card: click one card and confirm the real composer is populated or the normal action occurs.
- Project selector: click the real project chip under the “灵感基地” label and confirm the native project menu opens.
- Sidebar: open a real task, then return to New Task.
- Composer: type text, verify caret/readability, then clear it without sending.
- Reload: use CDP `Page.reload`, wait, and confirm the injection marker returns.
- Restore/reapply cycle: remove live skin, verify marker absent, apply again, verify marker present.
- Update resilience: resolve the current `OpenAI.Codex` Appx location dynamically; never store a versioned WindowsApps path.

## Visual checks

- 1280x820 initial home: CSS hero, two to four native cards, real project selector, and composer are visible without horizontal scrolling.
- Hero left copy remains readable; the right-side “ENFP 灵感小宇宙” decoration does not overlap native content.
- Suggestion cards use mint, coral, blue, and yellow accents while preserving native labels and icons.
- Narrower window: accept Codex's native responsive card reduction; no essential control is covered and the sticky note may intentionally hide.
- Normal task: messages remain readable and composer does not overlap content.
- Inspect sidebar, header, hero edges, card labels, composer controls, scrollbar, lightning ribbon, and sticky note.
- Reject black/transparent sidebar artifacts, clipped cards, duplicated/disconnected project labels, rasterized native controls, weak contrast, or decorations intercepting clicks.

## Exploratory checks

- Start when the debug port is occupied: fail with a clear message or use a caller-selected port.
- Start after Codex updates: package discovery and injection still work without patching installed files.
